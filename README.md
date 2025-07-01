# school-record-management-system
 
/*Done by:
1. Rana Kemal(RCD/2595/2016)
2. Nesiha Hussein(RCD/0880/2017) 
3. Remla kheyredin(RCD/0882/2017)
4. Mezida Delil(RCD/0876/2017)
5. Tesnim Esmael(Rmkd/0560/2017)
6. Nardos Fikadu(RCD/1714/2017)
*/


#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
using namespace std;

struct Student {
    string name;
    int id;
    int age;
    float gpa;

    Student(string n, int i, int a, float g) : name(n), id(i), age(a), gpa(g) {}
};

class SchoolSystem {
private:
    vector<Student> students;
    int nextId;

public:
    SchoolSystem() : nextId(1000) {}

    void addStudent() {
        string name;
        int age;
        float gpa;

        cout << "Enter student name: ";
        cin.ignore();
        getline(cin, name);
        cout << "Enter age: ";
        cin >> age;
        cout << "Enter GPA: ";
        cin >> gpa;

        students.push_back(Student(name, nextId++, age, gpa));
        cout << "Student added with ID: " << (nextId - 1) << endl;
    }

    void displayStudents() {
        if (students.empty()) {
            cout << "No students in the system." << endl;
            return;
        }

        cout << "\n--- Student Records ---" << endl;
        for (const auto& student : students) {
            cout << "ID: " << student.id << " | Name: " << student.name 
                 << " | Age: " << student.age << " | GPA: " << student.gpa << endl;
        }
    }

    void searchStudent() {
        int id;
        cout << "Enter student ID to search: ";
        cin >> id;

        for (const auto& student : students) {
            if (student.id == id) {
                cout << "Found - Name: " << student.name << ", Age: " 
                     << student.age << ", GPA: " << student.gpa << endl;
                return;
            }
        }
        cout << "Student not found." << endl;
    }

    void deleteStudent() {
        int id;
        cout << "Enter student ID to delete: ";
        cin >> id;

        auto it = remove_if(students.begin(), students.end(),
            [id](const Student& s) { return s.id == id; });

        if (it != students.end()) {
            students.erase(it, students.end());
            cout << "Student deleted successfully." << endl;
        } else {
            cout << "Student not found." << endl;
        }
    }

    void updateGPA() {
        int id;
        float newGPA;
        cout << "Enter student ID: ";
        cin >> id;

        for (auto& student : students) {
            if (student.id == id) {
                cout << "Enter new GPA: ";
                cin >> newGPA;
                student.gpa = newGPA;
                cout << "GPA updated successfully." << endl;
                return;
            }
        }
        cout << "Student not found." << endl;
    }
};

int main() {
    SchoolSystem school;
    int choice;

    while (true) {
        cout << "\n=== School Management System ===" << endl;
        cout << "1. Add Student" << endl;
        cout << "2. View All Students" << endl;
        cout << "3. Search Student" << endl;
        cout << "4. Delete Student" << endl;
        cout << "5. Update GPA" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice == 1) {
            school.addStudent();
        }
        else if (choice == 2) {
            school.displayStudents();
        }
        else if (choice == 3) {
            school.searchStudent();
        }
        else if (choice == 4) {
            school.deleteStudent();
        }
        else if (choice == 5) {
            school.updateGPA();
        }
        else if (choice == 6) {
            cout << "Thank you for using the system!" << endl;
            return 0;
        }
        else ({
            cout << "Invalid choice. Please try again." << endl;
        }
    }

    return 0;
}