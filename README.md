import java.util.Scanner;

public class SinemaSistemi {
    // Film bilgileri dizileri
    static String[] filmAdlari = new String[10];
    static int[] filmSuresi = new int[10];
    static String[] filmTurleri = new String[10];
    static int filmSayisi = 0;  // Maksimum 10 film

    // Müşteri bilgileri dizileri
    static String[] musteriAdlari = new String[20];
    static String[] musteriEmailAdresleri = new String[20];
    static int musteriSayisi = 0;  // Maksimum 20 müşteri

    // Bilet bilgileri dizisi (2D dizi: her müşteri için hangi film seçilmiş)
    static String[][] biletler = new String[20][10];  // 20 müşteri, her müşteri için 10 film
    static int[] biletSayisi = new int[20];  // Her müşteri için alınan bilet sayısı

    // Film ekleme
    public static void filmEkle(String filmAdi, int sure, String tur) {
        if (filmSayisi < 10) {
            filmAdlari[filmSayisi] = filmAdi;
            filmSuresi[filmSayisi] = sure;
            filmTurleri[filmSayisi] = tur;
            filmSayisi++;
            System.out.println(filmAdi + " filmi başarıyla eklendi.");
        } else {
            System.out.println("Maksimum film sayısına ulaşıldı.");
        }
    }

    // Müşteri kaydı
    public static void musteriEkle(String ad, String email) {
        if (musteriSayisi < 20) {
            musteriAdlari[musteriSayisi] = ad;
            musteriEmailAdresleri[musteriSayisi] = email;
            musteriSayisi++;
            System.out.println(ad + " başarıyla kaydedildi.");
        } else {
            System.out.println("Maksimum müşteri sayısına ulaşıldı.");
        }
    }

    // Bilet oluşturma
    public static void biletOlustur(int musteriIndex, int filmIndex) {
        if (musteriIndex < musteriSayisi && filmIndex < filmSayisi) {
            biletler[musteriIndex][biletSayisi[musteriIndex]] = filmAdlari[filmIndex];
            biletSayisi[musteriIndex]++;
            System.out.println(musteriAdlari[musteriIndex] + " için " + filmAdlari[filmIndex] + " filmi başarıyla bilet oluşturuldu.");
        } else {
            System.out.println("Geçersiz müşteri veya film.");
        }
    }

    // Biletleri listele
    public static void biletListele() {
        for (int i = 0; i < musteriSayisi; i++) {
            System.out.println(musteriAdlari[i] + " - Biletleri:");
            for (int j = 0; j < biletSayisi[i]; j++) {
                System.out.println("  " + biletler[i][j]);
            }
        }
    }

    // Film listeleme
    public static void filmListele() {
        System.out.println("Filmler Listesi:");
        for (int i = 0; i < filmSayisi; i++) {
            System.out.println(filmAdlari[i] + " - " + filmSuresi[i] + " dakika - Tür: " + filmTurleri[i]);
        }
    }

    // Müşteri listeleme
    public static void musteriListele() {
        System.out.println("Müşteriler Listesi:");
        for (int i = 0; i < musteriSayisi; i++) {
            System.out.println(musteriAdlari[i] + " - " + musteriEmailAdresleri[i]);
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n--- Sinema Sistemi ---");
            System.out.println("1. Film Ekle");
            System.out.println("2. Müşteri Ekle");
            System.out.println("3. Bilet Oluştur");
            System.out.println("4. Film Listele");
            System.out.println("5. Müşteri Listele");
            System.out.println("6. Biletleri Listele");
            System.out.println("7. Çıkış");
            System.out.print("Bir seçenek girin: ");
            int secim = scanner.nextInt();
            scanner.nextLine();  // Satır sonu karakterini temizle

            switch (secim) {
                case 1:
                    System.out.print("Film Adı: ");
                    String filmAdi = scanner.nextLine();
                    System.out.print("Film Süresi (dakika): ");
                    int sure = scanner.nextInt();
                    scanner.nextLine();  // Satır sonu karakterini temizle
                    System.out.print("Film Türü: ");
                    String tur = scanner.nextLine();
                    filmEkle(filmAdi, sure, tur);
                    break;

                case 2:
                    System.out.print("Müşteri Adı: ");
                    String ad = scanner.nextLine();
                    System.out.print("Müşteri Email Adresi: ");
                    String email = scanner.nextLine();
                    musteriEkle(ad, email);
                    break;

                case 3:
                    System.out.print("Müşteri Adı: ");
                    String musteriAd = scanner.nextLine();
                    int musteriIndex = -1;
                    for (int i = 0; i < musteriSayisi; i++) {
                        if (musteriAdlari[i].equals(musteriAd)) {
                            musteriIndex = i;
                            break;
                        }
                    }
                    if (musteriIndex == -1) {
                        System.out.println("Müşteri bulunamadı.");
                        break;
                    }
                    System.out.print("Film Adı: ");
                    String filmAdiBilet = scanner.nextLine();
                    int filmIndex = -1;
                    for (int i = 0; i < filmSayisi; i++) {
                        if (filmAdlari[i].equals(filmAdiBilet)) {
                            filmIndex = i;
                            break;
                        }
                    }
                    if (filmIndex == -1) {
                        System.out.println("Film bulunamadı.");
                        break;
                    }
                    biletOlustur(musteriIndex, filmIndex);
                    break;

                case 4:
                    filmListele();
                    break;

                case 5:
                    musteriListele();
                    break;

                case 6:
                    biletListele();
                    break;

                case 7:
                    System.out.println("Çıkılıyor...");
                    scanner.close();
                    return;

                default:
                    System.out.println("Geçersiz seçenek, lütfen tekrar deneyin.");
            }
        }
    }
}
