# UDTT
KTTX1
#include <iostream>
#include <vector>
#include <string>

using namespace std;

struct CongViec {
    string maCV;
    int thoiGianBatDau;
    double thoiGianThucHien; // th?i gian th?c hi?n tính theo phút ho?c gi?
};

vector<CongViec> c; // danh sách công vi?c
vector<string> L;    // danh sách nhân viên
int* x;              // m?ng dùng d? luu ch? s? khi quay lui

void KhoiTao() {
    c.push_back({"CV01", 8, 15});
    c.push_back({"CV02", 9, 45});
    c.push_back({"CV03", 10, 30});
    c.push_back({"CV04", 11, 60});
    c.push_back({"CV05", 13, 20});
    c.push_back({"CV06", 14, 25});
   
   L.push_back("NV01");
    L.push_back("NV02");
    L.push_back("NV03");
    L.push_back("NV04");
    L.push_back("NV05");
    L.push_back("NV06");
};

void HienThiCongViec(const CongViec& cv) {
    cout << "Ma CV: " << cv.maCV << ", Thoi gian bat dau: " << cv.thoiGianBatDau 
         << ", Thoi gian thuc hien: " << cv.thoiGianThucHien << " phut" << endl;
}

void HienThiNguoc(int n) {
    if (n < 0)
        return;
    HienThiCongViec(c[n]);
    HienThiNguoc(n - 1);
}

int DemCongViecNhoHon30(int l, int r) {
    if (l == r)
        return c[l].thoiGianThucHien <= 30 ? 1 : 0;
    int m = (l + r) / 2;
    return DemCongViecNhoHon30(l, m) + DemCongViecNhoHon30(m + 1, r);
}

void HienThiPhuongAn(int n) {
    for (int i = 0; i < n; i++) {
        cout << c[i].maCV << " - " << L[x[i] - 1] << "; ";
    }
    cout << endl;
}

void QuayLui(int n, int k) {
    if (k == n) {
        HienThiPhuongAn(n);
        return;
    }
    for (int i = 1; i <= n; i++) {
        bool ok = true;
        for (int j = 0; j < k; j++) {
            if (x[j] == i) {
                ok = false;
                break;
            }
        }
        if (ok) {
            x[k] = i;
            QuayLui(n, k + 1);
        }
    }
}

int main() {
    KhoiTao();
    
    cout << "Danh sach cong viec theo thu tu nguoc lai:" << endl;
    HienThiNguoc(c.size() - 1);

    cout << "\nSo cong viec co thoi gian thuc hien <= 30 phut: ";
    cout << DemCongViecNhoHon30(0, c.size() - 1) << endl;

    cout << "\nCac phuong an phan cong cong viec cho nhan vien:" << endl;
    x = new int[L.size()];
    QuayLui(c.size(), 0);
    delete[] x;

    return 0;
}
bay
#include<iostream>
#include<string>
#include<vector>

using namespace std;

struct chuyenbay{
	string sohieu;
	int giave;
	int soghe;
};
int *x;
vector<chuyenbay> cb;

void create(){
	cb.push_back(chuyenbay{"VN01",700000,25});
	cb.push_back(chuyenbay{"VN02",300000,25});
	cb.push_back(chuyenbay{"VN03",200000,25});
	cb.push_back(chuyenbay{"VN04",100000,25});
	cb.push_back(chuyenbay{"VN05",900000,25});
	cb.push_back(chuyenbay{"VN06",800000,25});
}
void hienthi(chuyenbay a){
	cout<<a.sohieu<<" "<<a.giave<<" "<<a.soghe<<endl;
}
void hienthigiave(int n){
	if(n<0){
		return;
	}
	if (cb.at(n).giave>700000)
		hienthi(cb.at(n));
	return hienthigiave(n-1);
}
chuyenbay chiadetri(int l,int r){
	if(l==r-1)
		return cb[l].giave>cb[r].giave ? cb[r]:cb[l];
	else if(l==r)
		return cb[l];
	else if(l<r){
	int m=(l+r)/2;
		return chiadetri(l,m).giave>chiadetri(m+1,r).giave ? chiadetri(m+1,r):chiadetri(l,m);
}

}
void hienthima(int k){
	 for(int i=0;i<k;i++)
	 	cout<<cb[x[i]-1].sohieu<<" ";
		 cout<<endl;
}
void quaylui(int n,int k,int i,int index){
	if(k==0){
		hienthima(index);
		return;
	}
	for(int j=i;j<n;j++)
		x[index=k]=j;
	quaylui(n,k-1,i+1,index);
}


int main(){
	create();
	hienthigiave(cb.size()-1);
	cout<<"min";
	x=new int[4];
	hienthi(chiadetri(0,cb.size()-1));
	quaylui(cb.size(),4,0,4);
}
