Untuk module `src/main/java` terdapat module `core`, `tiket`. Module tersebut berisikan function-function yang nantinya dapat dipanggil oleh test pada module `src/main/test`. 
## `src/main/java`
### `core`
Berisikan function umum yang akan digunakan baik di test maupun persiapan untuk test.

Contohnya, terdapat service untuk logging, membaca env, connect ke DB, dan lain sebagainya. Pelajari sebutuhnya aja yang perlu untuk ini.
### `tiket`
Di dalam module ini, terdapat module lagi berdasarkan verticalnya. Contohnya, terdapat module accomodation, b2b, flight, dan lain sebagainya.

Di dalam module vertical tersebut, terdapat spesifikasi untuk api, dto, dan pjo.

Di dalam folder api, terdapat api-api yang nantinya akan dipanggil pada test. Terdapat juga function verify untuk membandigkan expected result dengan result yang asli.