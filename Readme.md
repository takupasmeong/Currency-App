# Currency App
Aplikasi sederhana berbasis C# dengan fungsi mengkonversi nilai mata uang dollar($) ke Rupiah(Rp.) dimana value $1 = Rp.15.000 .

## Scope & Functionalities
- user dapat menginputkan nilai / value
- program hanya akan mengkonversi angka
- program akan menunjukkan pesan "Invalid" bila diberikan input selain angka

## How Does It works?
Pada method `MainWindow` di class MainWindow.xaml.cs, akan muncul secara otomatis function `InitializeComponent();`. kemudian dideklarasikan constructor dari class CurrencyController.cs. Berikut adalah tampilan source code method `MainWindow`.
```csharp
public MainWindow()
        {
            InitializeComponent();
            CurrencyController = new CurrencyController();
        }
```

Syntax untuk melakukan konversi terdapat pada class CurrencyController.cs. Dalam class CurrencyController, terdapat 2 public method yaitu `public string usdToIdr` dan `public boolean isAllowed`.
```csharp
class CurrencyController
    {
        public string usdToIdr(string nominal)
        {
            var nominalDouble = Convert.ToDouble(nominal);
            var result = nominalDouble * 15000;
            return Convert.ToString(result);
        }

        public Boolean isAllowed(string nominal)
        {
            Regex regex = new Regex("[^0-9.-]+");
            return !regex.IsMatch(nominal);
        }
    }
```

method `usdToIdr` berfungsi untuk mengkonversi nilai yang diinputkan dari bentuk string menjadi double sehingga dapat dikalikan dengan 15000. kemudian dikembalikan dalam bentuk string.

method `isAllowed` berfungsi untuk mencocokkan apakah inputan dari textbox sesuai dengan regular expression angka yang dideklarasikan.

pada method `Button_Hitung_Click` di class MainWindow.xaml.cs berfungsi untuk membaca inputan dari textbox dan untuk mengeluarkan hasil `result`. terdapat if else statement dengar parameter apabila karakter yang diinputkan pada textbox merupakan angka maka `result` akan berupa hasil konversi USD ke IDR. kemudian dikirim ke resultLabel.
```csharp
private void Button_Hitung_Click(object sender, RoutedEventArgs e)
        {
            var nominalInput = InputTextBox.Text;
            var result = "invalid";
            if (CurrencyController.isAllowed(nominalInput))
            {
                result = CurrencyController.usdToIdr(nominalInput);
            }
            resultLabel.Content = result;
        }
```

## Latihan

  - Mengapa perlu membuat class `CurrencyController.cs` pada percobaan 4 ?<br/>jawaban : Untuk memisahkan logic dari main source code sehingga codingan lebih rapih dan mudah untuk dirubah ketika akan melakukan pengembangan.
  - Jelaskan kegunaan method `isAllowed` pada percobaan 4!
    <br/>jawaban : method  `isAllowed`  berfungsi untuk mencocokkan apakah inputan dari textbox sesuai dengan regular expression angka yang dideklarasikan.
  - Jelaskan secara singkat mengenai Regex pada percobaan 4!
    <br/>jawaban : regex (regular expression) digunakan untuk memeriksa apakah sebuah string cocok dengan pola yang diberikan yaitu hanya dapat menerima inputan angka atau tidak.
  - Buatlah class diagramnya pada percobaan 4! 
  -<br/>jawaban : ![Alt text](D:/kuliah/semester-3/pemrograman-lanjut/classDiagram.jpg?raw=true "Title")