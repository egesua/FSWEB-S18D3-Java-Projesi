2) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    SELECT k.kitapadi t.turadi FROM kitap as k, tur AS t WHERE k.turno = t.turno AND t.turadi IN('Fikra','Hikaye') ORDER BY t.turadi, k.kitapadi;

3) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları listeleyin.

    SELECT o.ogrno, o.ograd, o.ogrsoyad, k.kitapadi, o.sinif FROM ogrenci AS o, kitap AS k, islem AS i WHERE o.ogrno = i.ogrno AND i.kitapno = k.kitapno AND o.sinif IN('10B','10C') ORDER BY o.ograd;

4) Öğrencinin adını, soyadını ve kitap aldığı tarihleri listeleyin.

    SELECT o.ad, o.soyad, i.atarih FROM ogrenci AS o INNER JOIN islem AS i ON o.ogreno = i.ogrno ORDER BY o.ograd;

5) Fıkra ve hikaye türündeki kitapların adını ve türünü listeleyin.

    SELECT k.kitapadi, t.turadi FROM kitap AS k INNER JOIN tur AS t ON k.turno = t.turno AND t.turadi IN ('Fikra','Hikaye');

6) 10B veya 10C sınıfındaki öğrencilerin numarasını, adını, soyadını ve okuduğu kitapları, öğrenci adına göre listeleyin.

   

7) Kitap alan öğrencinin adı, soyadı, kitap aldığı tarih listelensin. Kitap almayan öğrencilerinde listede görünsün.

   SELECT o.ograd, o.ogrsoyad, i.atarih FROM ogrenci AS o LEFT JOIN islem AS i ON o.ogrno = i.ogrno ORDER BY ASC;

8) Kitap almayan öğrencileri listeleyin.

    SELECT o.ograd, o.ogrsoyad, i.tarih FROM ogrenci AS o LEFT JOIN islem AS i ON o.ogrno = i.ogrno WHERE i.ogrno IS NULL;

9) Alınan kitapların kitap numarasını, adını ve kaç defa alındığını kitap numaralarına göre artan sırada listeleyiniz.

    SELECT i.kitapno, k.kitapadi, count(i.kitapno) AS TOTAL FROM islem AS i INNER JOIN kitap AS k ON i.kitapno = k.kitapno GROUP BY i.kitapno, k.kitapadi ORDER BY k.kitapno ASC;

10) Alınan kitapların kitap numarasını, adını kaç defa alındığını (alınmayan kitapların yanında 0 olsun) listeleyin.

    SELECT i.kitapno, k.kitapadi, count(i.kitapno) AS TOTAL FROM islem AS i INNER JOIN kitap AS k ON i.kitapno = k.kitapno GROUP BY i.kitapno, k.kitapadi ORDER BY TOTAL k.kitapno ASC;

11) Öğrencilerin adı soyadı ve aldıkları kitabın adı listelensin.

    SELECT o.ograd, o.ogrsoyad, k.kitapadi FROM ogrenci AS o INNER JOIN islem AS i ON o.ogrno = i.ogrno INNER JOIN kitap AS k ON k.kitapno = i.kitapno;

12) Her öğrencinin adı, soyadı, kitabın adı, yazarın adı soyad ve kitabın türünü ve kitabın alındığı tarihi listeleyiniz. Kitap almayan öğrenciler de listede görünsün.

    SELECT o.ograd, o.ogrsoyad, k.kitapadi, y.yazarad, y.yazarsoyad, i.atarih FROM ogrenci as o LEFT JOIN islem i ON o.ogrno = i.ogrno LEFT JOIN kitap AS k ON i.kitapno = k.kitapno LEFT JOIN yazar AS y ON k.yazarno = y.yazarno ORDER BY k.kitapadi DESC;

13) 10A veya 10B sınıfındaki öğrencilerin adı soyadı ve okuduğu kitap sayısını getirin.

    SELECT o.ograd, o.ogrsoyad, o.sinif, count(i.ogrno) AS TOTAL_READ FROM ogrenci AS o INNER JOIN islem AS i ON o.ogrno = i.ogrno WHERE o.sinif IN ('10A','10B') GROUP BY o.ograd, o.ogrsoyad, o.sinif ORDER BY TOTAL_READ DESC; 

14) Tüm kitapların ortalama sayfa sayısını bulunuz.
    
    SELECT AVG(k.sayfasayisi) FROM kitap as k;

15) Sayfa sayısı ortalama sayfanın üzerindeki kitapları listeleyin.

    SELECT * FROM kitap AS k WHERE k.sayfasayisi > (SELECT AVG(k.sayfasayisi) FROM kitap as k;

16) Öğrenci tablosundaki öğrenci sayısını gösterin

    SELECT COUNT(ogrno) FROM ogrenci;

17) Öğrenci tablosundaki toplam öğrenci sayısını toplam sayı takma(alias kullanımı) adı ile listeleyin.

    SELECT COUNT(ogrno) AS toplam FROM ogrenci;

18) Öğrenci tablosunda kaç farklı isimde öğrenci olduğunu listeleyiniz.

    SELECT count(DISTINCT ograd) as toplam FROM ogrenci;

19) En fazla sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    SELECT MAX(sayfasayisi) FROM kitap k;

20) En fazla sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    SELECT k.kitapadi, MAX(sayfasayisi) FROM kitap GROUP BY k.kitapadi;

21) En az sayfa sayısı olan kitabın sayfa sayısını listeleyiniz.

    SELECT MIN(sayfasayisi) FROM kitap k;

22) En az sayfası olan kitabın adını ve sayfa sayısını listeleyiniz.

    SELECT MIN(sayfasayisi) as minimum FROM kitap k;

23) Dram türündeki en fazla sayfası olan kitabın sayfa sayısını bulunuz.

    SELECT MAX(sayfasayisi) FROM kitap k INNER JOIN tur as t ON t.turno = k.turno WHERE t.turadi = 'Dram';

24) numarası 15 olan öğrencinin okuduğu toplam sayfa sayısını bulunuz.

    SELECT o.ograd, k.kitapadi FROM ogrenci as o INNER JOIN islem as i ON o.ogrno = i.ogrno INNER JOIN kitap as k ON i.kitapno = k.kitapno WHERE o.ogrno = 15;

25) İsme göre öğrenci sayılarının adedini bulunuz.(Örn: ali 5 tane, ahmet 8 tane )

    SELECT o.ograd, count(o.ogrno) FROM ogrenci AS o GROUP BY o.ograd;

26) Her sınıftaki öğrenci sayısını bulunuz.

    SELECT o.sinif,count(o.ogrno) FROM ogrenci AS o GROUP BY o.sinif;

27) Her sınıftaki erkek ve kız öğrenci sayısını bulunuz.

    SELECT o.sinif,count(o.ogrno) FROM ogrenci AS o GROUP BY o.cinsiyet;

28) Her öğrencinin adını, soyadını ve okuduğu toplam sayfa sayısını büyükten küçüğe doğru listeleyiniz.

    SELECT O.ograd, o.ogrsoyad, SUM(k.sayfasayisi) as OKUNAN_SAYFA_SAYISI FROM ogrenci AS o INNER JOIN islem as i ON o.ogrno = i.ogrno INNER JOIN kitap as k ON k.kitapno = i.kitapno GROUP BY o.ograd, o.ogrsoyad ORDER BY OKUNAN_SAYFA_SAYISI DESC; 

29) Her öğrencinin okuduğu kitap sayısını getiriniz.

    SELECT o.ograd, o.ogrsoyad, count(i.islemno) as okudugukitapsayisi FROM ogrenci as o INNER JOIN islem as i ON o.ogrno = i.ogrno GROUP BY o.ograd, o.ogrsoyad;