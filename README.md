#include <iostream>
#include <string>
using namespace std;

const int MAX = 100;

string names[MAX];
int balances[MAX];
int accountCount = 0; 

//출력만 할 때
void printBalance(int balance) {
    cout << balance << "원" << endl;
}

//  잔액 직접 변경
void deposit(int* balance, int amount) {
    *balance += amount;
}

void withdraw(int* balance, int amount) {
    *balance -= amount;
}

//  두 잔액 동시 변경
void transfer(int& from, int& to, int amount) {
    from -= amount;
    to += amount;
}

// 이름으로 인덱스 찾기, 없으면 -1 반환
int findAccount(string name) {
    for (int i = 0; i < accountCount; i++) {
        if (names[i] == name) return i;
    }
    return -1;
}

void printMenu() {
    cout << "\n============ 은행 계좌 관리 시스템 ============" << endl;
    cout << "1. 현재 등록된 계좌 리스트 보기" << endl;
    cout << "2. 신규 계좌 등록" << endl;
    cout << "3. 입금 및 출금" << endl;
    cout << "4. 계좌 간 이체" << endl;
    cout << "5. 프로그램 종료" << endl;
    cout << "================================================" << endl;
    cout << ">> 메뉴 선택 : ";
}

void showAccounts() {
    cout << "\n--------- [현재 등록된 계좌 리스트] ---------" << endl;
    if (accountCount == 0) {
        cout << "(등록된 계좌가 없습니다.)" << endl;
    }
    else {
        for (int i = 0; i < accountCount; i++) {
            cout << i + 1 << ". 이름 : " << names[i]
                << "\t\t| 잔액 : " << balances[i] << "원" << endl;
        }
    }
    cout << "---------------------------------------------" << endl;
}

void registerAccount() {
    cout << "\n[신규 계좌 등록]" << endl;
    cout << "등록할 이름 : ";
    cin >> names[accountCount];
    cout << "초기 잔액 : ";
    cin >> balances[accountCount];
    accountCount++;
    cout << "신규 계좌 등록 완료했습니다." << endl;
}

void depositWithdraw() {
    string name;
    cout << "\n조회할 이름을 입력하세요 : ";
    cin >> name;

    int idx = findAccount(name);
    if (idx == -1) {
        cout << "존재하지 않는 사용자입니다." << endl;
        return;
    }

    cout << "현재 " << name << "님의 잔액 : ";
    printBalance(balances[idx]);  

    int choice;
    cout << "(1) 입금  |  (2) 출금 : ";
    cin >> choice;

    if (choice != 1 && choice != 2) {
        cout << "올바른 번호를 입력하세요 (1 또는 2)." << endl;
        return;
    }

    int amount;
    cout << "거래 금액 입력 : ";
    cin >> amount;

    if (choice == 1) {
        deposit(&balances[idx], amount);  
        cout << amount << "원 입금 완료했습니다." << endl;
    }
    else {
        if (balances[idx] < amount) {
            cout << "잔액이 부족합니다." << endl;
        }
        else {
            withdraw(&balances[idx], amount);  
            cout << amount << "원 출금 완료했습니다." << endl;
        }
    }
}

void transferBetween() {
    cout << "미구현;";
}

int main() {
    int choice;

    while (true) {
        printMenu();
        cin >> choice;

        if (choice == 1) showAccounts();
        else if (choice == 2) registerAccount();
        else if (choice == 3) depositWithdraw();
        else if (choice == 4) transferBetween();
        else if (choice == 5) {
            cout << "프로그램을 종료합니다." << endl;
            break;
        }
        else {
            cout << "올바른 번호를 입력해주세요." << endl;
        }
    }

    return 0;
}
