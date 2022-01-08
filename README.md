# hospital_management_system
this is a source code for hospital management system based on oop in c++

```
#include <iostream>
#include <string>
using namespace std;

const int K = 2, D = 3, n = 15;
//n=patient , D=pharmacy , K=inspect_kind

class Hospital {
private:
	string Name_Hospital, Place, History;
	int Num_Of_ambulance, Storey, Num_Of_Doctor_one_storey, Num_Of_Room_one_storey;
	int  Total_Employe, Total_sister, Total_Doctor;
public:
	int Room;
	Hospital() { }
	Hospital(string Name, string history, string Place, int Storey, int Num_Of_Doctor_one_storey, int Num_Of_Room_one_storey, int Num_Of_ambulance) {
		this->Num_Of_Doctor_one_storey = Num_Of_Doctor_one_storey;
		this->Num_Of_Room_one_storey = Num_Of_Room_one_storey;
		this->Num_Of_ambulance = Num_Of_ambulance;
		this->Name_Hospital = Name;
		this->History = history;
		this->Place = Place;
		this->Storey = Storey;
		Room = Storey * Num_Of_Room_one_storey;
		Total_Doctor = Storey * Num_Of_Doctor_one_storey;
		Total_sister = Total_Doctor * 2;
		Total_Employe = Num_Of_Room_one_storey + Num_Of_Doctor_one_storey;

	}

	void Display_Hospital_Info() {
		cout << "\n\tName:-----------------> " << Name_Hospital << "<-----------------\n";
		cout << "\tHistory: " << History << endl;
		cout << "\tPlace: " << Place << endl;
		cout << "\tStorey: " << Storey << endl;
		cout << "\tRoom: " << Room << endl;
		cout << "\t  Total_Doctor: " << Total_Doctor << endl;
		cout << "\t  Total_sister: " << Total_sister << endl;
		cout << "\t  Total_Employe: " << Total_Employe << endl;
	}

	int Set_Total_Doctor() { return Total_Doctor; }
	int Set_Total_Sister() { return Total_sister; }
	int Set_Total_Employe() { return Total_Employe; }

};//End Class Hospital

class Person {
protected:
	string* Address, * Name, * Gender, * specializ;
	int* Age, * Number_Phone, * ID, * Salary, * Room_person;

public:
	Person() {}

	~Person() {
		delete[]Name;
		delete[]Gender;
		delete[]Age;
		delete[]Number_Phone;
		delete[]ID;
		delete[]Salary;
		delete[]Room_person;
		delete[]Address;
	}
};

class Doctor :public Person {
private:

	int Num_specializ_Doctor;
	//as nashem bihaya bi dema array di constructore da jbar hinde min dynamic bkarenna
public:
	static int Total_Salary_Doctor;
	Doctor() {}
	Doctor(Hospital H) {//i get a object because i dont can get total doctor in inheretamce 0
		//if i get friend har de objecte chekam lawa
		Name = new string[H.Set_Total_Doctor()];
		Number_Phone = new int[H.Set_Total_Doctor()];
		ID = new int[H.Set_Total_Doctor()];
		Gender = new string[H.Set_Total_Doctor()];
		Salary = new int[H.Set_Total_Doctor()];
		Age = new int[H.Set_Total_Doctor()];
		Room_person = new int[H.Set_Total_Doctor()];

		cout << "\n-------------> Total Doctor is <-------------{ " << H.Set_Total_Doctor() << " }------------->" << endl;
		for (int i = 0; i < H.Set_Total_Doctor(); i++)
		{
			cout << "\t  Enter Name of Doctor [" << i << "]: ";
			cin >> Name[i];
			cout << "\tAge is : ";
			cin >> Age[i];
			cout << "\tID is : ";
			cin >> ID[i];
			cout << "\tNumber of phone is : ";
			cin >> Number_Phone[i];
			cout << "\tGender must be male or female: ";
			cin >> Gender[i];
			while (Gender[i] != "male" && Gender[i] != "female")
			{
				cout << "pleas make soure you typet Gender corect: ";
				cin >> Gender[i];
			}
			cout << "\tRoom bettween [0] To [" << H.Room << "] : ";
			cin >> Room_person[i];
			cout << "\t  number of specialization Doctor " << Name[i] << " is : ";
			cin >> Num_specializ_Doctor;
			specializ = new string[Num_specializ_Doctor];
			for (int j = 0; j < Num_specializ_Doctor; j++)
			{
				cout << "\t Enter specialization " << j << " of " << Name[i] << ": ";
				cin >> specializ[j];
			}
			cout << "\tSalary " << Name[i] << " is: ";
			cin >> Salary[i];

			Total_Salary_Doctor = Total_Salary_Doctor + Salary[i];
		}
	}//end construcor

	void Print_Info_Doctor(Hospital H) {
		for (int i = 0; i < H.Set_Total_Doctor(); i++)
		{
			cout << "\t  Name Doctor [" << i << "] is: " << Name[i] << endl;
			cout << "\tID Doctor [" << Name[i] << "] is: " << ID[i] << endl;
			cout << "\tAge Doctor [" << Name[i] << "] is: " << Age[i] << endl;
			cout << "\tNumber of Phone Doctor [" << Name[i] << "] is: " << Number_Phone[i] << endl;
			cout << "\tGender Doctor [" << Name[i] << "] is: " << Gender[i] << endl;
			for (int j = 0; j < Num_specializ_Doctor; j++)
				cout << "\t  It is specializ the " << Name[i] << " is: " << specializ[j] << "\n\n";
		}
	}
	void Set_Total_Salaray_Doctor() { cout << "Total Salary is:" << Total_Salary_Doctor; }

	friend void Get_Doctor_ID(Hospital&, Doctor&);

};//end Class Doctor

void Get_Doctor_ID(Hospital& H, Doctor& D) {
	int id;
	cout << "\t\tEnter ID of Doctor Doyo want to Get info: ";	cin >> id;
	for (int i = 0; i < H.Set_Total_Doctor(); i++) {
		if (id == D.ID[i])
		{
			cout << "\n\t  **********************\n\t  Name Doctor is: " << D.Name[i] << endl;
			cout << "\tIt is ID is: " << D.ID[i] << endl;
			cout << "\tIt is Age is: " << D.Age[i] << endl;
			cout << "\tNumber of Phone Doctor is: " << D.Number_Phone[i] << endl;
			cout << "\tGender is: " << D.Gender[i] << endl;
			cout << "\tsalary is: " << D.Salary[i] << endl;
			for (int j = 0; j < D.Num_specializ_Doctor; j++)
				cout << "\tIt is specializ the " << D.Name[i] << " is: " << D.specializ[j] << endl;
		}
		else { cout << "\t  ID undefine!!\n"; }
	}
	cout << "\t  **********************\n\n";
}/////////////////////////////////////////////////////////////End Friend Function_Doctor

class Sister :public Person {
public:
	static int Total_Salary_Sister;
public:
	Sister() {}
	Sister(Hospital H) {
		Name = new string[H.Set_Total_Sister()];
		Age = new int[H.Set_Total_Sister()];
		Address = new string[H.Set_Total_Sister()];
		ID = new int[H.Set_Total_Sister()];
		Gender = new string[H.Set_Total_Sister()];
		Salary = new int[H.Set_Total_Sister()];

		cout << "\n\t  -------------> Total Sister is <-------------{ " << H.Set_Total_Sister() << " }------------->" << endl;
		for (int i = 0; i < H.Set_Total_Sister(); i++)
		{
			cout << "\n\t  Enter Name of Sister [" << i << "]: ";
			cin >> Name[i];
			cout << "\tID is : ";
			cin >> ID[i];
			cout << "\tAddress is : ";
			cin >> Address[i];
			cout << "\tAge is : ";
			cin >> Age[i];
			cout << "\tGender is: ";
			cin >> Gender[i];
			cout << "\tSalary is: ";
			cin >> Salary[i];
			cout << "\tspecializ is: ";
			cin >> specializ[i];

			Total_Salary_Sister = Total_Salary_Sister + Salary[i];
		}
	}

	void Print_Info_Sister(Hospital H) {
		for (int i = 0; i < H.Set_Total_Sister(); i++)
		{
			cout << "\t  Name Sister [" << i << "] is: " << Name[i] << endl;
			cout << "\tID Sister [" << i << "] is: " << ID[i] << endl;
			cout << "\tAddress Sister is: " << Address[i] << endl;
			cout << "\tAge Sister [" << i << "] is: " << Age[i] << endl;
			cout << "\tGender Sister [" << i << "] is: " << Gender[i] << endl;
			cout << "\tIt is Salary the is: " << Salary[i] << endl;
			cout << "\tIt is specializ the is: " << specializ[i] << endl;
		}
		cout << "\tIt is Total Salary the is: " << Total_Salary_Sister << "\n\n";
	}

	void Set_Total_Salaray_Sister() { cout << "\tTotal Salary is:" << Total_Salary_Sister << endl; }

	friend void Get_Sister_ID(Hospital&, Sister&);

};

void Get_Sister_ID(Hospital& H, Sister& S) {
	int id;
	cout << "\t  Enter ID of Sister Doyo want to Get info: ";  cin >> id;
	for (int i = 0; i < H.Set_Total_Sister(); i++) {
		if (id == S.ID[i])
		{
			cout << "\n\t**********************\n\t  Name Sister is: " << S.Name[i] << endl;
			cout << "\tID Sister is: " << S.ID[i] << endl;
			cout << "\tAddress Sister is: " << S.Address[i] << endl;
			cout << "\tAge Sister is: " << S.Age[i] << endl;
			cout << "\tGender Sister is: " << S.Gender[i] << endl;
			cout << "\tSalary sister is: " << S.Salary[i] << endl;
		}
		cout << "\t**********************\n\n";
	}
}////////////////////////////////////////////////////End Friend Function_Sister

class Employee :public Doctor {//i can not inheretance to person beause name-age..same name doctor
public:
	static int Total_Salary_Employe;
public:
	Employee() {}
	Employee(Hospital H) {
		Name = new string[H.Set_Total_Employe()];
		Age = new int[H.Set_Total_Employe()];
		ID = new int[H.Set_Total_Employe()];
		Gender = new string[H.Set_Total_Employe()];
		Salary = new int[H.Set_Total_Employe()];
		specializ = new string[H.Set_Total_Employe()];

		cout << "\n\t  -------------> Total Employe is <-------------{ " << H.Set_Total_Employe() << " }------------->" << endl;
		for (int i = 0; i < H.Set_Total_Employe(); i++)
		{
			cout << "\n\t  Enter Name of Employe [" << i << "]: ";
			cin >> Name[i];
			cout << "\tID is : ";
			cin >> ID[i];
			cout << "\tAge is : ";
			cin >> Age[i];
			cout << "\tGender is: ";
			cin >> Gender[i];
			cout << "\tWork Employee is: ";
			cin >> specializ[i];
			cout << "\tSalary is: ";
			cin >> Salary[i];

			Total_Salary_Employe = Total_Salary_Employe + Salary[i];
		}
	}//End Constructor

	void Print_Info_Employe(Hospital H) {
		for (int i = 0; i < H.Set_Total_Employe(); i++)
		{
			cout << "\n\t  Name Employee [" << i << "] is: " << Name[i] << endl;
			cout << "\tID  [" << i << "] is: " << ID[i] << endl;
			cout << "\tAge  [" << i << "] is: " << Age[i] << endl;
			cout << "\tGender [" << i << "] is: " << Gender[i] << endl;
			cout << "\tIt is salary : " << Salary[i] << endl;
			cout << "\tIt is work : " << specializ[i] << endl;
		}
		cout << "\tIt is Total Salary the is: " << Total_Salary_Employe << "\n\n";
	}

	void Set_Total_Salaray_Employe() { cout << "Total Salary is:" << Total_Salary_Employe << endl; }
	friend void Get_Employe_ID(Hospital&, Employee&);

};//end class employee

void Get_Employe_ID(Hospital& H, Employee& E) {
	int id;
	cout << "\tEnter ID of Employe Doyo want to Get info: ";  cin >> id;
	for (int i = 0; i < H.Set_Total_Employe(); i++)
	{
		if (id == E.ID[i])
		{
			cout << "\n\t  **********************\n\t  Name Employe is: " << E.Name[i] << endl;
			cout << "\tID Employe is: " << E.ID[i] << endl;
			cout << "\tAge Employe is: " << E.Age[i] << endl;
			cout << "\tGender Employe is: " << E.Gender[i] << endl;
			cout << "\tSalary Employe is: " << E.Salary[i] << endl;
			cout << "\tWork Employe is: " << E.specializ[i] << endl;
		}
		cout << "\t  **********************\n\n";
	}
}///////////////////////////////////////////////////////////End Feiend_Function_Employe

class Patient {
private:
	string Name[n], Gender[n], Sick[n], Blood[n];
	int Age[n], Number_Phone[n];
	static int Front, Rear;
	// n is global scope
public:
	void insert(string Name, int Age, int Number_Phone, string Gender, string Sick, string Blood) {
		if (Full())
			cout << "\tQueue is Full\n";

		else {
			Rear++;
			this->Name[Rear] = Name;
			this->Sick[Rear] = Sick;
			this->Blood[Rear] = Blood;
			this->Age[Rear] = Age;
			this->Number_Phone[Rear] = Number_Phone;
			this->Gender[Rear] = Gender;
		}
	}

	int Full() {
		if (Rear == n)	return 1;
		else		return 0;
	}

	void Remov() {
		string P, G, S, B;
		int Pho, A;
		if (Empty())
			cout << "\tQueue is Empty";
		else {
			Front++;
			P = Name[Front];
			S = Sick[Front];
			B = Blood[Front];
			G = Gender[Front];
			Pho = Number_Phone[Front];
			A = Age[Front];
		}
	}

	int Empty() {
		if (Rear == Front)	return 1;
		else	return 0;
	}

	void Print() {
		if (Empty())
			cout << "\tQueue is Empty \n";
		else
			for (int i = Front + 1; i <= Rear; i++)
				cout << Name[i] << "  " << Age[i] << "  " << Blood[i] << "  " << Sick[i] << "  " << Number_Phone[i] << "  " << Gender[i] << "\t\t";
	}

	int Start() {
		Patient People;
		int Choice, Total, age, number_phone;
		string name, gender, sick, blood;
		cout << "\n\t   *********************\n";
		cout << "\t   1 - insert ifo The People in the Queue \n";
		cout << "\t   2- remov People Info in the Queue \n";
		cout << "\t   3- Print ifo The People in the Queue \n";
		cout << "\t   4- Exit Queue Patient \n\t   *********************\n";
		cout << "\n\t    Enter the Choice: ";
		cin >> Choice;
		while (Choice != 4)
		{
			if (Choice == 1)
			{
				cout << "\tHow many paient do you want to insert queue: ";
				cin >> Total;
				for (int i = 1; i <= Total; i++)
				{
					cout << "\t  Inserting the Patient " << i << " name:";
					cin >> name;
					cout << "\tInserting the Blood it :";
					cin >> blood;
					cout << "\tInserting the Age it :";
					cin >> age;
					cout << "\tInserting the Sick of it :";
					cin >> sick;
					cout << "\tInserting the Number of Phone :";
					cin >> number_phone;
					cout << "\tInserting the Gender Maile or Femail :";
					cin >> gender;

					People.insert(name, age, number_phone, gender, sick, blood);
					cout << endl;
				}
			}
			if (Choice == 2)
			{
				cout << "How many paient doyo wand to Remov queue: ";
				cin >> Total;
				for (int i = 1; i <= Total; i++)
					People.Remov();
			}
			if (Choice == 3)
				People.Print();

			cout << "\n\tin Queue Enter another choice: ";
			cin >> Choice;
		}//end While
		return 0;
	}//end Statr Function

};//////////////////////////////////////////////////////////////////end class Queue

class pharmacy :public Hospital {
protected:
	string medicament[D];
	double price[D];
	string PRO[D];
	string EXP[D];
public:
	pharmacy() {
		cout << "\n\t  enter info pharmsy\n";
		for (int i = 0; i < D; i++)
		{
			cout << "\tenter medicament" << i << ": ";
			cin >> medicament[i];
			cout << "\tenter Price:  ";
			cin >> price[i];
			cout << "\tenter Product:  ";
			cin >> PRO[i];
			cout << "\tenter Expire:  ";
			cin >> EXP[i];
		}
	}

	void Set_medicament_Name()
	{
		string k;
		cout << "\t  Enter the KInd info do you want learn about: \n";
		for (int i = 0; i < D; i++) {
			cout << " \tinspect Kind " << i << " : " << medicament[i] << endl;
		}
		cin >> k;
		for (int i = 0; i < D; i++) {
			if (medicament[i] == k) {
				cout << "\tmedicament is: " << medicament[i] << "\t Price: " << price[i];
				cout << "\t Time Product: " << PRO[i] << "\t Time Expire: " << EXP[i] << endl;
			}
		}
	}
};////////////////////////////////////////end class Pharmacy

class inspect {
private:
	string kind[K];
	double time[K];
	double price[K];
public:
	inspect()
	{
		for (int i = 0; i < K; i++) {
			cout << "Enter inspect Kind [ " << i << " ]: ";
			cin >> kind[i];
			cout << "Enter inspect time:";
			cin >> time[i];
			cout << "Enter inspect price:";
			cin >> price[i];
		}
	}
	void set_inspect_kind()
	{
		string k;
		cout << "Enter the KInd info do you want learn about: \n";
		for (int i = 0; i < K; i++) {
			cout << " inspect Kind " << i << " : " << kind[i] << endl;
		}
		cin >> k;
		for (int i = 0; i < K; i++) {
			if (kind[i] == k)
				cout << "Kind is: " << kind[i] << "\t Time: " << time[i] << "\t Price: " << price[i] << endl;
		}
	}
};////////////////////////////////////////End inspect class

class Stor :public pharmacy {
private:
	int blood_d, zxt_d, sugar_d;
	int Total_jh = 0;
	static int count;

	//
	//
	void stor_inspect() {
		blood_d = 10;
		zxt_d = 8;
		sugar_d = 5;

		cout << "Total Blood Device in store is: " << blood_d << endl;
		cout << "Total zukht Device in store is: " << zxt_d << endl;
		cout << "Total sugar Device in store is: " << sugar_d << endl;
		count = count + (blood_d + zxt_d + sugar_d);

		if (Total_jh > count)    cout << "Store is full!!!\n";
		else   cout << "we have empty " << count - Total_jh << endl;
	}

	void Stor_Pharmacy() {
		int c = 0;
		const int SP = 6;
		medicament[SP];
		EXP[SP];
		PRO[SP];
		cout << "Total count medicament in Store is {" << SP << "}\n";
		for (int i = 0; i < SP; i++)
		{
			cout << "\tenter medicament [" << i << "]: ";
			cin >> medicament[i];
			cout << "\tenter Product:  ";
			cin >> PRO[i];
			cout << "\tenter Expire:  ";
			cin >> EXP[i];
		}
		for (int i = 0; i < SP; i++)
		{
			if (EXP[i] < "2019/27/11")
				c++;
		}
		cout << "total expire is: " << c;
		count += count + SP;

		if (Total_jh > count)    cout << "Store is full!!!\n";
		else   cout << "we have empty " << count - Total_jh << endl;
	}

	void Get_Total_Mony_Hospital(Doctor D, Employee E, Sister S) {
		cout << "any mony: " << D.Total_Salary_Doctor + E.Total_Salary_Employe + S.Total_Salary_Sister;
	}

};


int Patient::Rear = 0;
int Patient::Front = 0;
int Sister::Total_Salary_Sister = 0;
int Doctor::Total_Salary_Doctor = 0;
int Employee::Total_Salary_Employe = 0;
int Stor::count = 50;

int main()
{
	cout << "\n\n\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n";
	cout << "\t@@ _______________________________________________________________ @@\n";
	cout << "\t@@|                                                               |@@\n";
	cout << "\t@@|                        WELCOME TO                             |@@\n";
	cout << "\t@@|                                                               |@@\n";
	cout << "\t@@|                 HOSPITAL MANAGEMENT SYSTEM                    |@@\n";
	cout << "\t@@|                                                               |@@\n";
	cout << "\t@@|          by:Hamdi & Omeed & Anas & Hajivan & Zakia            |@@\n";
	cout << "\t@@|                                                               |@@\n";
	cout << "\t@@|                                                               |@@\n";
	cout << "\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n";

	Hospital H("Barwari", "2019/27/11", "Kurdistan", 1, 2, 12, 8);
	int Choice;
	cout << "\n\t\t  HOSPITAL MANAGEMENT SYSTEM \n\n";
	cout << "\n\n  Please,  Choose from the following Options: \n";
	cout << "\t _________________________________________________________________ \n";
	cout << "\t|             1  >> Get all Information About Hospital            |\n";
	cout << "\t|             2  >> About Doctor                                  |\n";
	cout << "\t|             3  >> Queue And Info For Patient                    |\n";
	cout << "\t|             4  >> About Sister                                  |\n";
	cout << "\t|             5  >> About Employe                                 |\n";
	cout << "\t|             6  >> Pharmacy Room                                 |\n";
	cout << "\t|             7  >> inspect  Room                                 |\n";
	cout << "\t|             8  >> Exit Hospital Management                      |\n";
	cout << "\t|_________________________________________________________________|\n\n";
	cout << "\t  Enter your choice: "; cin >> Choice;

	while (Choice != 8)
	{
		if (Choice == 1)
			H.Display_Hospital_Info();
		if (Choice == 2)
		{
			int Ch;
			Doctor D(H);
			cout << "\n\n\t  <-------------------->\n";
			cout << "\t  1-To Get The doctor with ID \n";
			cout << "\t  2- Print All info for Doctor \n";
			cout << "\t  3- Total Salary For Doctor in Hospital \n";
			cout << "\t  4- Exit About Doctor\n\t  <-------------------->";
			cout << "\n\t    Enter the choice: ";
			cin >> Ch;
			while (Ch != 4) {

				if (Ch == 1)
					Get_Doctor_ID(H, D);

				if (Ch == 2)
					D.Print_Info_Doctor(H);

				if (Ch == 3)
					D.Set_Total_Salaray_Doctor();

				cout << "\n\t    in { Doctor } Enter another choice: ";
				cin >> Ch;
			}
			false;
		}//end doctor if

		if (Choice == 3) {
			Patient P;
			P.Start();
		}//end patient 

		if (Choice == 4)
		{
			int Ch;
			Sister S(H);
			cout << "\n\n<-------------------->\n";
			cout << "\t  1- To Get The Sister with ID \n";
			cout << "\t  2- Print All info for Sister \n";
			cout << "\t  3- Total Salary For Sister in Hospital \n";
			cout << "\t  4- Exit Management Sister\n<-------------------->\n";
			cout << "\t  Enter the choice: ";
			cin >> Ch;
			while (Ch != 4) {
				if (Ch == 1)
					Get_Sister_ID(H, S);
				if (Ch == 2)
					S.Print_Info_Sister(H);
				if (Ch == 3)
					S.Set_Total_Salaray_Sister();

				cout << "\n\t   in { Sister } Enter another choice: ";
				cin >> Ch;
			}
			false;
		}//end if sister

		if (Choice == 5)
		{
			int Ch;
			Employee E(H);
			cout << "\n\n<-------------------->\n";
			cout << "\t  1- To Get The Employe with ID \n";
			cout << "\t  2- Print All info for Employe \n";
			cout << "\t  3- Total Salary For Employe in Hospital \n";
			cout << "\t  4- Exit management Employe\n<-------------------->\n";
			cout << "\t  Enter the choice: ";
			cin >> Ch;
			while (Ch != 4) {
				if (Ch == 1)
					Get_Employe_ID(H, E);//Friend
				if (Ch == 2)
					E.Print_Info_Employe(H);
				if (Ch == 3)
					E.Set_Total_Salaray_Employe();

				cout << "\n\t   in {Employee} Enter another choice: ";
				cin >> Ch;
			}
			false;
		}//end if employee

		if (Choice == 6)
		{
			int Ch;
			pharmacy ph;
			cout << "\n\n\t  <-------------------->\n";
			cout << "\t  1- Set medicament Name To get info about it\n";
			cout << "\t  2- Exit Pharmacy Room\n\t  <-------------------->\n";
			cout << "\t  Enter the choice: ";
			cin >> Ch;
			while (Ch != 2) {
				if (Ch == 1)
					ph.Set_medicament_Name();

				cout << "\n\t   in {Pharmacy} Enter another choice: ";
				cin >> Ch;
			}
			false;
		}//end if pharmacy


		if (Choice == 7)
		{
			int Ch;
			inspect I;
			cout << "\n\t  <-------------------->\n";
			cout << "\t  1- Set inspect kind To get info about it\n";
			cout << "\t  2- Exit inspect Room\n\t  <-------------------->\n";
			cout << "\t  Enter the choice: ";
			cin >> Ch;
			while (Ch != 2) {
				if (Ch == 1)
					I.set_inspect_kind();

				cout << "\n\t  in {inspect} Enter another choice: ";
				cin >> Ch;
			}
			false;
		}//end if pharmacy

		cout << "\n\t\t    >>>>> Main Choice  Enter another choise: ";
		cin >> Choice;
	}//end Main While 
	return 0;
}

```


