public abstract class SanPham
{
    private string maSanPham;
    private string tenSanPham;
    private double giaSanPham;

    public string MaSanPham
    {
        get { return maSanPham; }
        set { maSanPham = value; }
    }

    public string TenSanPham
    {
        get { return tenSanPham; }
        set { tenSanPham = value; }
    }

    public double GiaSanPham
    {
        get { return giaSanPham; }
        set { giaSanPham = value; }
    }

    public SanPham(string maSanPham, string tenSanPham, double giaSanPham)
    {
        this.maSanPham = maSanPham;
        this.tenSanPham = tenSanPham;
        this.giaSanPham = giaSanPham;
    }

    public abstract double TinhTongTien();

    public override string ToString()
    {
        return string.Format("{0,-15} {1,-20} {2,-15}", maSanPham, tenSanPham, giaSanPham);
    }
}
he
public class SanPhamThanhLy : SanPham
{
    private double donGia;
    private int soLuong;

    public double DonGia
    {
        get { return donGia; }
        set { donGia = value; }
    }

    public int SoLuong
    {
        get { return soLuong; }
        set { soLuong = value; }
    }

    public SanPhamThanhLy(string maSanPham, string tenSanPham, double giaSanPham, double donGia, int soLuong)
        : base(maSanPham, tenSanPham, giaSanPham)
    {
        this.donGia = donGia;
        this.soLuong = soLuong;
    }

    public override double TinhTongTien()
    {
        return donGia * soLuong;
    }

    public override string ToString()
    {
        return base.ToString() + string.Format(" {0,-15} {1,-10} {2,-15}", donGia, soLuong, TinhTongTien());
    }
}
he
public class Program
{
    static List<SanPhamThanhLy> danhSachSanPham = new List<SanPhamThanhLy>();

    static void Main(string[] args)
    {
        bool thoat = false;
        do
        {
            Console.WriteLine("1. Nhap thong tin san pham");
            Console.WriteLine("2. Hien thi danh sach san pham");
            Console.WriteLine("3. Sua thong tin san pham");
            Console.WriteLine("4. Thoat");
            Console.Write("Nhap lua chon cua ban: ");
            string luaChon = Console.ReadLine();

            switch (luaChon)
            {
                case "1":
                    NhapThongTinSanPham();
                    break;
                case "2":
                    HienThiDanhSachSanPham();
                    break;
                case "3":
                    SuaThongTinSanPham();
                    break;
                case "4":
                    thoat = true;
                    break;
                default:
                    Console.WriteLine("Lua chon khong hop le. Vui long thu lai.");
                    break;
            }
        }
        while (!thoat);
    }

    static void NhapThongTinSanPham()
    {
        Console.Write("Nhap ma san pham: ");
        string maSanPham = Console.ReadLine();
        Console.Write("Nhap ten san pham: ");
        string tenSanPham = Console.ReadLine();
        Console.Write("Nhap gia san pham: ");
        double giaSanPham = double.Parse(Console.ReadLine());
        Console.Write("Nhap don gia: ");
        double donGia = double.Parse(Console.ReadLine());
        Console.Write("Nhap so luong: ");
        int soLuong = int.Parse(Console.ReadLine());

        SanPhamThanhLy sanPham = new SanPhamThanhLy(maSanPham, tenSanPham, giaSanPham, donGia, soLuong);
        danhSachSanPham.Add(sanPham);
    }

    static void HienThiDanhSachSanPham()
    {
        Console.WriteLine("{0,-15} {1,-20} {2,-15} {3,-15} {4,-10} {5,-15}", "Ma SP", "Ten SP", "Gia SP", "Don Gia", "So Luong", "Tong Tien");
        foreach (var sanPham in danhSachSanPham)
        {
            Console.WriteLine(sanPham.ToString());
        }
    }

    static void SuaThongTinSanPham()
    {
        Console.Write("Nhap ma san pham can sua: ");
        string maSanPham = Console.ReadLine();
        
        SanPhamThanhLy sanPham = danhSachSanPham.FirstOrDefault(sp => sp.MaSanPham == maSanPham);
        if (sanPham != null)
        {
            Console.Write("Nhap don gia moi: ");
            sanPham.DonGia = double.Parse(Console.ReadLine());
            Console.Write("Nhap so luong moi: ");
            sanPham.SoLuong = int.Parse(Console.ReadLine());
            Console.WriteLine("Da cap nhat thong tin san pham.");
        }
        else
        {
            Console.WriteLine("Khong tim thay san pham co ma nhu tren.");
        }
    }
}
