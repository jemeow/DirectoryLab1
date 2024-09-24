#include <iostream>
#include <direct.h> 
#include <string>

using namespace std;

void list_file();
void directory();
void change_dir();

int main() {
    int input;
    while (true) {
        cout << "--------------------------------\n";
		cout << "\tMain Menu" << endl;
        cout << "--------------------------------\n";
        cout << "1. To Display List of Files\n";
        cout << "2. To Create New Directory\n";
        cout << "3. To Change the Working Directory\n";
        cout << "4. Exit\n";
        cout << "Enter Number: ";
        cin >> input;

        switch (input) {
            case 1:
                list_file();
                break;
            case 2:
                directory();
                break;
            case 3:
                change_dir();
                break;
            case 4:
                return 0;
            default:
                cout << "Invalid input. Please try again......\n";
        }
    }
    return 0;
}

void list_file() {
    int input;
    cout << "--------------------------------";
    cout << "\n     LIST FILE DETAIL:" << endl;
    cout << "--------------------------------\n";
    cout << "1. List All Files\n";
    cout << "2. List of Extension Files\n";
    cout << "3. List of Name Wise\n";
    cout << "Enter Number: ";
    cin >> input;

    switch (input) {
        case 1:
            cout << "List of all (*.*) Files\n";
            system("dir");
            break;
        case 2: {
            string ext;
            cout << "Enter file extension: ";
            cin >> ext;
            system(("dir *." + ext).c_str());
            break;
        }
        case 3: {
            string pattern;
            cout << "Enter file name pattern: ";
            cin >> pattern;
            system(("dir " + pattern).c_str());
            break;
        }
        default:
            cout << "Invalid choice. Please try again.\n";
    }
}

void directory() {
    string dir;
    cout << "Directory name: ";
    cin >> dir;

    if (_mkdir(dir.c_str()) == 0) {
        cout << "Directory created.\n";
    } else {
        cout << "Error creating directory. It may already exist or invalid.\n";
    }
}

void change_dir() {
    int command;
    cout << "Current Directory:" << endl;
    cout << "1. Step by Step Backward\n" << endl;
    cout << "2. Go to Root Directory\n" << endl;
    cout << "3. Forward Directory\n" << endl;
    cout << "Enter number: ";
    cin >> command;

    if (command == 1) {
            if (_chdir("..") == 0) {
                cout << "Moved to parent directory." << endl;
            } else {
                cout << "Error! Could not move to parent directory." << endl;
            }
        }else if (command == 2){
            if (_chdir("\\") == 0) {
                cout << "Moved to root directory." << endl;
            } else {
                cout << "Error! Could not move to root directory." << endl;
            }
        } else if (command == 3){
            string dir;
            cout << "Directory name: ";
            cin >> dir;
            if (_chdir(dir.c_str()) == 0) {
                cout << "Directory has changed successfully!" << endl;
            } else {
                cout << "Error changing directory. Does not exist.." << endl;
            }
            }else {
        	cout << "Invalid, Please Try again......" << endl;
}
}
