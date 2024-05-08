# n
#include<iostream>
#include<iomanip>
#include<string.h>
#include<fstream>
#include<map>
using namespace std;

// product Class includes all the functions that can be applied to the products in the store.
class Product{
  private:
    int Id;
    string Name;
    int Inventory;
    double Price;
    static int key ;
    
  public:
 // product constructor
    Product(string na="" ,int in=0, double pr=0):Name(na),Inventory(in),Price(pr){
    Id=key+1;
    }
     ~Product(){}
     
// getters and setters
    int get_Id() {
      return Id;  
    }
    string  get_Name(){
      return Name;
    }
    
    int get_Inventory() {
        return Inventory;
      }
    double get_Price(){
        return Price;
      }
      
    void set_Id(int id){
      Id=id;
    }
    void set_Name(string name){
      Name=name;
    }
    void set_Inventory(int inventory){
      Inventory=inventory;
    }
    void set_Price(double price){
      Price=price;
    }
//This function suggests what products to add to the store according to the product inventory
void suggestaddingproduct(map<int,Product>& products ){
    for( auto& pair : products){
    if(pair.second.Inventory<10){
        int j=1;
  if(j==1)
cout<<"The inventory of these products is less than ten, it is better to add them to your store first.\n";
      cout<<"**_"<<pair.second.get_Name()<<"  with inventory: "<<pair.second.Inventory<<"\n";
      j++;
    }
    else{
      cout<<"All products have inventory above ten.\n";
    }
    }
}
//    This function is for adding products to the store
    void productinsert(Product& p, map<int,Product>& products ){
      if(!products.empty())
       for( auto& pair : products)
      if (pair.second.get_Name()==p.Name){
        string answer="";
        cout<<"The name of the product is repeated . Are you sure you want to add it?(yee/no)";
        cin>>answer;
        if(answer=="no"){
        return ;
        }
      }
    key++;
    products[p.Id]=p;  
      }
//This function edits the product information according to the user's choice    
  void Productedit(string name, map<int,Product>& products){
    for( auto& pair : products){
       if(pair.second.get_Name()==name){
    int editoption;
    cout<<"What do you want to edit from the product? {1.name; 2.inventory; 3.price}(select your number)";
    cin>>editoption;
    
    switch(editoption){
    case 1:
    {
      string newname;
      cout << "Enter new name: ";
          cin >> newname;
      products[pair.first].set_Name(newname);
      break;
    }
    case 2:
    {
      int newinventory;
      cout << "Enter new inventory: ";
          cin >> newinventory;
       products[pair.first].set_Inventory(newinventory);
       break;
    }
    case 3:
    {
    double newprice;
    cout << "Enter new price: ";
        cin >> newprice;    
    products[pair.first].set_Price(newprice);
    break;    
    }
    default:
    cout<<"Invalid choice. Please try again.\n";
      break;
    }
       cout << "Product with ID " << pair.first << " has been updated successfully." << endl;
            return;
        }
    }
    cout << "Product with  this Name   not found in the products." << endl;
}
//This function shows the products to the user  
    void showproduct(map<int,Product>& products){
  if(!products.empty()){
  
  cout<<"Id "<<setw(20)<<"Name "<<setw(15)<<"Inventory "<<setw(10)<<"Price "<<"\n";
  string line(120,'_');
  cout<<line<<"\n";
  for( auto& pair : products)
    cout<<pair.second.get_Id()<<setw(20)<<pair.second.get_Name()<<setw(10)<<pair.second.get_Inventory()<<setw(15)<<pair.second.get_Price()
  <<setw(10)<<"\n";
      cout<<line<<"\n";
      cout<<"\n"<<"\n";
      }
  }
};