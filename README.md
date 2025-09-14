# disha
#include <iostream>
#include <vector>
#include <string>

using namespace std;

class Student {
private:
    int rollNumber;
    string name;
    float marks;

public:
    Student(int r, string n, float m) : rollNumber(r), name(n), marks(m) {}

    int getRollNumber() const {
        return rollNumber;
    }

    void display() const {
        cout << "Roll No: " << rollNumber << ", Name: " << name << ", Marks: " << marks << endl;
    }
};

class StudentManager {
private:
    vector<Student> students;

public:
    void addStudent() {
        int roll;
        string name;
        float marks;

        cout << "Enter Roll Number: ";
        cin >> roll;
        cout << "Enter Name: ";
        cin.ignore();
        getline(cin, name);
        cout << "Enter Marks: ";
        cin >> marks;

        students.emplace_back(roll, name, marks);
        cout << "Student added successfully!\n";
    }

    void displayStudents() const {
        if (students.empty()) {
            cout << "No students to display.\n";
            return;
        }

        for (const auto& s : students) {
            s.display();
        }
    }

    void searchStudent() const {
        int roll;
        cout << "Enter Roll Number to search: ";
        cin >> roll;

        for (const auto& s : students) {
            if (s.getRollNumber() == roll) {
                s.display();
                return;
            }
        }

        cout << "Student with Roll No " << roll << " not found.\n";
    }
};

int main() {
    StudentManager manager;
    int choice;

    do {
        cout << "\n----- Student Management Menu -----\n";
        cout << "1. Add Student\n2. Display All Students\n3. Search Student by Roll Number\n4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                manager.addStudent();
                break;
            case 2:
                manager.displayStudents();
                break;
            case 3:
                manager.searchStudent();
                break;
            case 4:
                cout << "Exiting program.\n";
                break;
            default:
                cout << "Invalid choice. Try again.\n";
        }

    } while (choice != 4);

    return 0;
}
