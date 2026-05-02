# Cryptography-Task-3-4

Мета роботи: Дослiдження особливостей реалiзацiї цифрового пiдпису та сертифiкатiв

Виконання роботи: 
- Іван Лукʼянець: Виконання пунктів 4-8, написання звіту
- Андрій Бойчук: 

 
## Завдання Практичної роботи

1. Була реалізована геш-функцiя SHA-256. Детальний код реалізації можна побачити у файлі task_3_4.ipynb Також була проведена перевірка коректності згідно з [тестовими векторами](https://di-mgt.com.au/sha_testvectors.html)
   
```
assert sha256(b"abc") == "ba7816bf 8f01cfea 414140de 5dae2223 b00361a3 96177a9c b410ff61 f20015ad".replace(" ", ""), 'Test Case for "abc" failed'

assert sha256(b"") == "e3b0c442 98fc1c14 9afbf4c8 996fb924 27ae41e4 649b934c a495991b 7852b855".replace(" ", ""), 'Test Case for "" failed'

assert sha256(b"abcdbcdecdefdefgefghfghighijhijkijkljklmklmnlmnomnopnopq") == "248d6a61 d20638b8 e5c02693 0c3e6039 a33ce459 64ff2167 f6ecedd4 19db06c1".replace(" ", ""), 'Test Case for "abcdbcdecdefdefgefghfghighijhijkijkljklmklmnlmnomnopnopq" failed'

assert sha256(b"abcdefghbcdefghicdefghijdefghijkefghijklfghijklmghijklmnhijklmnoijklmnopjklmnopqklmnopqrlmnopqrsmnopqrstnopqrstu") == "cf5b16a7 78af8380 036ce59e 7b049237 0b249b11 e8f07a51 afac4503 7afee9d1".replace(" ", ""), 'Test Case for "abcdefghbcdefghicdefghijdefghijkefghijklfghijklmghijklmnhijklmnoijklmnopjklmnopqklmnopqrlmnopqrsmnopqrstnopqrstu" failed'

assert sha256(b"a" * 1000000) == "cdc76e5c 9914fb92 81a1c7e2 84d73e67 f1809a48 a497200e 046d39cc c7112cd0".replace(" ", ""), 'Test Case for "a" * 1000000 failed'a

assert sha256(b"abcdefghbcdefghicdefghijdefghijkefghijklfghijklmghijklmnhijklmno" * 16777216) == "50e72a0e 26442fe2 552dc393 8ac58658 228c0cbf b1d2ca87 2ae43526 6fcd055e".replace(" ", ""), 'Test Case for "abcdefghbcdefghicdefghijdefghijkefghijklfghijklmghijklmnhijklmno" * 16,777,216 failed'


print("Tests were successfull!!!")
```

2. Підбір префікса був здійснений методом повного перебору допоки не знайдеться префікс, який після функції видає 32 бітових нулі, тобто 4 байти нулі на початку повідомлення.\
Отриманий префікс: b'\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x9b\xdf\x14J'. \
Кількість ітерацій: 2615088203.
В алгоритмі кожен префікс дорівнював номеру ітерації, щоб не було можливих перетинів через використання `urandom()`. Також використовував бібліотечну імплементацію шифру, бо він реалізований не на чистому пайтоні, що робить пошук швидше. В результаті пошук зайняв більше години.

3. За допомогою команд OpenSSL створили власну пару відкритого та секретного ключа. Їх можна побачити у файлі server.key. Запит до центру сертифiкацiї у файлі server.csr. Самопідписаний сертифікат у server.crt. Усі команди та дослідження вмісту можна побачити у вже згаданому файлі, task_3_4.ipynb.

4. Передали запит на формування сертифiкату service.csr до іншої команди, яка його підписала. У результаті отримали сертифікат підписаний не нами.(файл our_team_server_signed.crt). Також допомогли іншій команді виконати це завдання.(файл server_utkin_korcheniuk_signed.crt) Команди та дослідження цього сертифікату можна побачити у ноутбуці.

5. Створив файл pizza.txt потім з використанням openssl підписав це повідомлення схемою RSA-PSS. Отримали pizza_signed.bin. Проблема "textbook RSA" це детермінованість підпису для одного й того самого повідомлення. Також ще одним мінусом є це атака мультиплікативності: sign(m1) * sign(m2) = sign(m1 * m2), коли ми зможемо підсовувати інші повідомлення. Пілся впровадження схеми RSA-PSS ми вводимо в структуру сіль, яка вводить невизначиність. Тому цей падінг вирішує проблему ці дві проблеми. У першому випадку ми будемо отримувати кожний раз різне повідомлення, а з мультиплікативність не буде працювати бо з рандомною частиною ми не зможемо відтворити цю матиматичну властивість Enc(m1) * Enc(m2) = (m1^e * m2^e) mod n = (m1 * m2)^e mod n = Enc(m1 * m2).

6. Для шифрування цього повідомлення, дістаємо відкритий ключ з самопідписаного сертифікату через команду openssl. Потім використовуємо цей ключ для шифрування. У результаті маємо повідомлення pizza_encrypted.bin, код у ноутбуці.

7. <img width="1710" height="988" alt="Знімок екрана 2026-05-02 о 22 23 33" src="https://github.com/user-attachments/assets/139e15a9-55f8-4776-b0ae-49d9a3d4fb64" /> Діяв трохи менше 3 місяців з 2021-06-19	по 2021-09-17.

8. <img width="1710" height="988" alt="Знімок екрана 2026-05-02 о 22 30 22" src="https://github.com/user-attachments/assets/139f778c-5df6-4ed2-936f-800b13af5958" /> Знайшли активний сертифікат kse.ua. Тут можна побачити його відбиток(геш-значення для SHA-256 і SHA-1). Ці відбитки обчислюються як геш функція від сертифікату. Тому завантажив сертифікат на цьому сайті(червона стрілочка). Після цього для знаходження коректного відбитку, треба перевести сертифікат у файловий тип der, який дозволяє зробити це правильно. Після відповідних кроків ми отримали ідентичний відбиток до того який у нашому файлі.





