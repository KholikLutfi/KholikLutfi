from mysql.connector import connect, Error
import os
import mysql.connector

# koneksi dengan database
def koneksi():
    koneksidb = None
    try:
        koneksidb = connect(
            host = "localhost",
            user = "root",
            passwd = "",
            database = "toko"
        )
        print("Berhasil terkoneksi dengan database!")
    except Error as e:
        print(e)
    return koneksidb
# koneksi()


def tampilData(conn):
    query = "SELECT * FROM barang "

    with conn.cursor() as cur:
        cur.execute(query)
        result = cur.fetchall()
        for row in result:
            print(row)
# tampilData(koneksi())

def tambahData(conn,data):
    query = "INSERT INTO barang(kode,nama_barang,harga) VALUES (%s,%s,%s)"

    try:
        with conn.cursor() as cur:
            cur.execute(query,data)
            conn.commit()
            print("Barang berhasil ditambahkan!")
    except Error as e:
        print(e)

dataBarang = ("9J8I", "Isolatip", 7000)
# tambahData(koneksi(),dataBarang)
# tampilData(koneksi())


def ubahData(conn,data):
    query = "UPDATE SET barang nama_barang=%s,harga=%s, WHERE kode=%s"

    try:
        with conn.cursor() as cur:
            cur.execute(query,data)
            conn.commit()
            print("Barang berhasil diubah!")
    except Error as e:
        print(e)
dataBaru = ("Spidol",10000,"DR08")
ubahData(koneksi(),dataBaru)
