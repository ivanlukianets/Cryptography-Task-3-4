# Cryptography-Task-3-4

Мета роботи: Дослiдження особливостей реалiзацiї цифрового пiдпису та сертифiкатiв

Виконання роботи: 
- Іван Лукʼянець: 
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

2. Підбір префікса

3. За допомогою команд OpenSSL створили власну пару відкритого та секретного ключа. Їх можна побачити у файлі server.key. Запит до центру сертифiкацiї у файлі server.csr. Самопідписаний сертифікат у server.crt. Усі команди та дослідження вмісту можна побачити у вже згаданому файлі, task_3_4.ipynb.

4. 


