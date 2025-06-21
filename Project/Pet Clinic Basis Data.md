```sql
CREATE TABLE users (
    email           VARCHAR(50) PRIMARY KEY,
    password        VARCHAR(100) NOT NULL,
    alamat          TEXT         NOT NULL,
    nomor_telepon   VARCHAR(15)  NOT NULL
);

/* ------------------------------------------------------------------
   2. PEGAWAI
   ------------------------------------------------------------------*/
CREATE TABLE pegawai (
    no_pegawai            UUID        PRIMARY KEY,
    tanggal_mulai_kerja   DATE        NOT NULL,
    tanggal_akhir_kerja   DATE,
    email_user            VARCHAR(50) NOT NULL REFERENCES users(email)
);

/* ------------------------------------------------------------------
   3. KLIEN
   ------------------------------------------------------------------*/
CREATE TABLE klien (
    no_identitas        UUID        PRIMARY KEY,
    tanggal_registrasi  DATE        NOT NULL,
    email               VARCHAR(50) NOT NULL REFERENCES users(email)
);

/* ------------------------------------------------------------------
   4. INDIVIDU
   ------------------------------------------------------------------*/
CREATE TABLE individu (
    no_identitas_klien UUID PRIMARY KEY REFERENCES klien(no_identitas),
    nama_depan         VARCHAR(50) NOT NULL,
    nama_tengah        VARCHAR(50),
    nama_belakang      VARCHAR(50) NOT NULL
);

/* ------------------------------------------------------------------
   5. PERUSAHAAN
   ------------------------------------------------------------------*/
CREATE TABLE perusahaan (
    no_identitas_klien UUID PRIMARY KEY REFERENCES klien(no_identitas),
    nama_perusahaan    VARCHAR(100) NOT NULL
);

/* ------------------------------------------------------------------
   6. TENAGA_MEDIS  (common ancestor for dokter/perawat)
   ------------------------------------------------------------------*/
CREATE TABLE tenaga_medis (
    no_tenaga_medis  UUID PRIMARY KEY REFERENCES pegawai(no_pegawai),
    no_izin_praktik  VARCHAR(20) UNIQUE NOT NULL
);

/* ------------------------------------------------------------------
   7. FRONT_DESK
   ------------------------------------------------------------------*/
CREATE TABLE front_desk (
    no_front_desk UUID PRIMARY KEY REFERENCES pegawai(no_pegawai)
);

/* ------------------------------------------------------------------
   8. DOKTER_HEWAN
   ------------------------------------------------------------------*/
CREATE TABLE dokter_hewan (
    no_dokter_hewan UUID PRIMARY KEY REFERENCES tenaga_medis(no_tenaga_medis)
);

/* ------------------------------------------------------------------
   9. PERAWAT_HEWAN
   ------------------------------------------------------------------*/
CREATE TABLE perawat_hewan (
    no_perawat_hewan UUID PRIMARY KEY REFERENCES tenaga_medis(no_tenaga_medis)
);

/* ------------------------------------------------------------------
   10. SERTIFIKAT_KOMPETENSI
      (composite PK of (no_sertifikat_kompetensi, no_tenaga_medis))
   ------------------------------------------------------------------*/
CREATE TABLE sertifikat_kompetensi (
    no_sertifikat_kompetensi VARCHAR(10),
    no_tenaga_medis         UUID,
    nama_sertifikat         VARCHAR(100) NOT NULL,
    PRIMARY KEY (no_sertifikat_kompetensi, no_tenaga_medis),
    FOREIGN KEY (no_tenaga_medis) REFERENCES tenaga_medis(no_tenaga_medis)
);

/* ------------------------------------------------------------------
   11. JENIS_HEWAN
   ------------------------------------------------------------------*/
CREATE TABLE jenis_hewan (
    id          UUID PRIMARY KEY,
    nama_jenis  VARCHAR(50) NOT NULL
);

/* ------------------------------------------------------------------
   12. HEWAN  (composite PK: nama + no_identitas_klien)
   ------------------------------------------------------------------*/
CREATE TABLE hewan (
    nama                VARCHAR(50),
    no_identitas_klien  UUID,
    tanggal_lahir       DATE NOT NULL,
    id_jenis            UUID NOT NULL REFERENCES jenis_hewan(id),
    url_foto            VARCHAR(255) NOT NULL,
    PRIMARY KEY (nama, no_identitas_klien),
    FOREIGN KEY (no_identitas_klien) REFERENCES klien(no_identitas)
);

/* ------------------------------------------------------------------
   13. VAKSIN
   ------------------------------------------------------------------*/
CREATE TABLE vaksin (
    kode  VARCHAR(6)  PRIMARY KEY,
    nama  VARCHAR(50) NOT NULL,
    harga INT         NOT NULL,
    stok  INT         NOT NULL
);

/* ------------------------------------------------------------------
   14. OBAT
   ------------------------------------------------------------------*/
CREATE TABLE obat (
    kode   VARCHAR(10) PRIMARY KEY,
    nama   VARCHAR(100) NOT NULL,
    harga  INT          NOT NULL,
    stok   INT          NOT NULL,
    dosis  TEXT         NOT NULL
);

/* ------------------------------------------------------------------
   15. PERAWATAN
   ------------------------------------------------------------------*/
CREATE TABLE perawatan (
    kode_perawatan  VARCHAR(10) PRIMARY KEY,
    nama_perawatan  VARCHAR(100) NOT NULL,
    biaya_perawatan INT          NOT NULL
);

/* ------------------------------------------------------------------
   16. PERAWATAN_OBAT  (composite PK)
   ------------------------------------------------------------------*/
CREATE TABLE perawatan_obat (
    kode_perawatan  VARCHAR(10),
    kode_obat       VARCHAR(10),
    kuantitas_obat  INT NOT NULL,
    PRIMARY KEY (kode_perawatan, kode_obat),
    FOREIGN KEY (kode_perawatan) REFERENCES perawatan(kode_perawatan),
    FOREIGN KEY (kode_obat)      REFERENCES obat(kode)
);

/* ------------------------------------------------------------------
   17. JADWAL_PRAKTIK  (composite PK)
   ------------------------------------------------------------------*/
CREATE TABLE jadwal_praktik (
    no_dokter_hewan UUID,
    hari            VARCHAR(10),
    jam             VARCHAR(20),
    PRIMARY KEY (no_dokter_hewan, hari, jam),
    FOREIGN KEY (no_dokter_hewan) REFERENCES dokter_hewan(no_dokter_hewan)
);

/* ------------------------------------------------------------------
   18. KUNJUNGAN  (composite PK over 7 attributes)
   ------------------------------------------------------------------*/
CREATE TABLE kunjungan (
    id_kunjungan       UUID,
    nama_hewan         VARCHAR(50),
    no_identitas_klien UUID,
    no_front_desk      UUID,
    no_perawat_hewan   UUID,
    no_dokter_hewan    UUID,
    kode_vaksin        VARCHAR(6),
    tipe_kunjungan     VARCHAR(10) NOT NULL,
    timestamp_awal     TIMESTAMP   NOT NULL,
    timestamp_akhir    TIMESTAMP,
    suhu               INT,
    berat_badan        NUMERIC(5,2),
    PRIMARY KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ),
    FOREIGN KEY (nama_hewan, no_identitas_klien)
        REFERENCES hewan(nama, no_identitas_klien),
    FOREIGN KEY (no_front_desk)    REFERENCES front_desk(no_front_desk),
    FOREIGN KEY (no_perawat_hewan) REFERENCES perawat_hewan(no_perawat_hewan),
    FOREIGN KEY (no_dokter_hewan)  REFERENCES dokter_hewan(no_dokter_hewan),
    FOREIGN KEY (kode_vaksin)      REFERENCES vaksin(kode)
);

/* ------------------------------------------------------------------
   19. KUNJUNGAN_KEPERAWATAN  (composite PK mirrors KUNJUNGAN + kode_perawatan)
   ------------------------------------------------------------------*/
CREATE TABLE kunjungan_keperawatan (
    id_kunjungan       UUID,
    nama_hewan         VARCHAR(50),
    no_identitas_klien UUID,
    no_front_desk      UUID,
    no_perawat_hewan   UUID,
    no_dokter_hewan    UUID,
    kode_perawatan     VARCHAR(10),
    catatan            TEXT,
    PRIMARY KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan,
        kode_perawatan
    ),
    FOREIGN KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ) REFERENCES kunjungan(
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ),
    FOREIGN KEY (kode_perawatan) REFERENCES perawatan(kode_perawatan)
);
```

## SQLite DDL Query
```sql
PRAGMA foreign_keys = ON;

CREATE TABLE users (
    email               TEXT PRIMARY KEY, -- VARCHAR(50) becomes TEXT, length not enforced by DB
    password            TEXT NOT NULL,    -- VARCHAR(100) becomes TEXT
    alamat              TEXT NOT NULL,
    nomor_telepon       TEXT NOT NULL     -- VARCHAR(15) becomes TEXT
);

CREATE TABLE pegawai (
    no_pegawai          TEXT PRIMARY KEY,
    tanggal_mulai_kerja DATE NOT NULL,
    tanggal_akhir_kerja DATE,
    email_user          TEXT NOT NULL REFERENCES users(email)
);

CREATE TABLE klien (
    no_identitas        TEXT PRIMARY KEY,
    tanggal_registrasi  DATE NOT NULL,
    email               TEXT NOT NULL REFERENCES users(email)
);

CREATE TABLE individu (
    no_identitas_klien TEXT PRIMARY KEY REFERENCES klien(no_identitas),
    nama_depan         TEXT NOT NULL,
    nama_tengah        TEXT,            
    nama_belakang      TEXT NOT NULL   
);

CREATE TABLE perusahaan (
    no_identitas_klien TEXT PRIMARY KEY REFERENCES klien(no_identitas),
    nama_perusahaan    TEXT NOT NULL
);

CREATE TABLE tenaga_medis (
    no_tenaga_medis TEXT PRIMARY KEY REFERENCES pegawai(no_pegawai), 
    no_izin_praktik TEXT UNIQUE NOT NULL 
);

CREATE TABLE front_desk (
    no_front_desk TEXT PRIMARY KEY REFERENCES pegawai(no_pegawai)
);

CREATE TABLE dokter_hewan (
    no_dokter_hewan TEXT PRIMARY KEY REFERENCES tenaga_medis(no_tenaga_medis)
);

CREATE TABLE perawat_hewan (
    no_perawat_hewan TEXT PRIMARY KEY REFERENCES tenaga_medis(no_tenaga_medis)
);

CREATE TABLE sertifikat_kompetensi (
    no_sertifikat_kompetensi TEXT,
    no_tenaga_medis          TEXT,
    nama_sertifikat          TEXT NOT NULL,
    PRIMARY KEY (no_sertifikat_kompetensi, no_tenaga_medis),
    FOREIGN KEY (no_tenaga_medis) REFERENCES tenaga_medis(no_tenaga_medis)
);


CREATE TABLE jenis_hewan (
    id          TEXT PRIMARY KEY, 
    nama_jenis  TEXT NOT NULL  
);

CREATE TABLE hewan (
    nama                TEXT,
    no_identitas_klien  TEXT, 
    tanggal_lahir       DATE NOT NULL,
    id_jenis            TEXT NOT NULL REFERENCES jenis_hewan(id), 
    url_foto            TEXT NOT NULL, 
    PRIMARY KEY (nama, no_identitas_klien),
    FOREIGN KEY (no_identitas_klien) REFERENCES klien(no_identitas)
);

CREATE TABLE vaksin (
    kode TEXT PRIMARY KEY,
    nama TEXT NOT NULL,   
    harga INTEGER NOT NULL,
    stok  INTEGER NOT NULL 
);

CREATE TABLE obat (
    kode  TEXT PRIMARY KEY,  
    nama  TEXT NOT NULL,    
    harga INTEGER NOT NULL,
    stok  INTEGER NOT NULL,  
    dosis TEXT NOT NULL
);

CREATE TABLE perawatan (
    kode_perawatan  TEXT PRIMARY KEY, 
    nama_perawatan  TEXT NOT NULL,     
    biaya_perawatan INTEGER NOT NULL   
);

CREATE TABLE perawatan_obat (
    kode_perawatan TEXT,
    kode_obat      TEXT, 
    kuantitas_obat INTEGER NOT NULL,
    PRIMARY KEY (kode_perawatan, kode_obat),
    FOREIGN KEY (kode_perawatan) REFERENCES perawatan(kode_perawatan),
    FOREIGN KEY (kode_obat)      REFERENCES obat(kode)
);

CREATE TABLE jadwal_praktik (
    no_dokter_hewan TEXT,
    hari            TEXT, 
    jam             TEXT,
    PRIMARY KEY (no_dokter_hewan, hari, jam),
    FOREIGN KEY (no_dokter_hewan) REFERENCES dokter_hewan(no_dokter_hewan)
);

CREATE TABLE kunjungan (
    id_kunjungan       TEXT,
    nama_hewan         TEXT, 
    no_identitas_klien TEXT, 
    no_front_desk      TEXT, 
    no_perawat_hewan   TEXT, 
    no_dokter_hewan    TEXT, 
    kode_vaksin        TEXT, 
    tipe_kunjungan     TEXT NOT NULL, 
    timestamp_awal     DATETIME NOT NULL,
    timestamp_akhir    DATETIME,          
    suhu               INTEGER,           
    berat_badan        REAL,             
    PRIMARY KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ),
    FOREIGN KEY (nama_hewan, no_identitas_klien)
        REFERENCES hewan(nama, no_identitas_klien),
    FOREIGN KEY (no_front_desk)    REFERENCES front_desk(no_front_desk),
    FOREIGN KEY (no_perawat_hewan) REFERENCES perawat_hewan(no_perawat_hewan),
    FOREIGN KEY (no_dokter_hewan)  REFERENCES dokter_hewan(no_dokter_hewan),
    FOREIGN KEY (kode_vaksin)      REFERENCES vaksin(kode)
);

CREATE TABLE kunjungan_keperawatan (
    id_kunjungan       TEXT, 
    nama_hewan         TEXT,
    no_identitas_klien TEXT, 
    no_front_desk      TEXT,
    no_perawat_hewan   TEXT, 
    no_dokter_hewan    TEXT, 
    kode_perawatan     TEXT, 
    catatan            TEXT,
    PRIMARY KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan,
        kode_perawatan
    ),
    FOREIGN KEY (
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ) REFERENCES kunjungan(
        id_kunjungan,
        nama_hewan,
        no_identitas_klien,
        no_front_desk,
        no_perawat_hewan,
        no_dokter_hewan
    ),
    FOREIGN KEY (kode_perawatan) REFERENCES perawatan(kode_perawatan)
);
```