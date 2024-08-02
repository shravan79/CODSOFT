#CODSOFT 




                                                       TASK 1 
                                              NUMBER GUESSING GAME 
#include <iostream>
#include <cstdlib>
#include <ctime>

int main() {
    
    srand(static_cast<unsigned int>(time(nullptr)));

    
    int secretNumber = rand() % 50 + 1;

    
    int attempts = 0;

    
    while (true) {
        
        int guess;
        std::cout << "Guess a number between 1 and 50: ";
        std::cin >> guess;

       
        attempts++;

       
        if (guess == secretNumber) {
            std::cout << " Congratulations! You found the number in " << attempts << " attempts.\n";
            break;
        }
       
        else if (guess > secretNumber) {
            std::cout << "Too high! Try again.\n";
        }
        
        else {
            std::cout << "Too low! Try again.\n";
        }
    }

    return 0;
}






                                                                      TASK 2 
                                                               SIMPLE CALCULATOR 


    #include <iostream>


double add(double num1, double num2) {
    return num1 + num2;
}


double subtract(double num1, double num2) {
    return num1 - num2;
}


double multiply(double num1, double num2) {
    return num1 * num2;
}


double divide(double num1, double num2) {
    if (num2 == 0) {
        throw std::runtime_error("Cannot divide by zero!");
    }
    return num1 / num2;
}

int main() {
    double num1, num2;
    char operation;

    
    std::cout << "Simple Calculator\n";
    std::cout << "-----------------\n";
    std::cout << "1. Addition (+)\n";
    std::cout << "2. Subtraction (-)\n";
    std::cout << "3. Multiplication (*)\n";
    std::cout << "4. Division (/)\n";
    std::cout << "Enter your choice (1-4): ";

    
    int choice;
    std::cin >> choice;

    
    std::cout << "Enter first number: ";
    std::cin >> num1;
    std::cout << "Enter second number: ";
    std::cin >> num2;

    
    switch (choice) {
        case 1:
            operation = '+';
            std::cout << num1 << " " << operation << " " << num2 << " = " << add(num1, num2) << std::endl;
            break;
        case 2:
            operation = '-';
            std::cout << num1 << " " << operation << " " << num2 << " = " << subtract(num1, num2) << std::endl;
            break;
        case 3:
            operation = '*';
            std::cout << num1 << " " << operation << " " << num2 << " = " << multiply(num1, num2) << std::endl;
            break;
        case 4:
            operation = '/';
            try {
                std::cout << num1 << " " << operation << " " << num2 << " = " << divide(num1, num2) << std::endl;
            } catch (const std::exception& e) {
                std::cerr << e.what() << std::endl;
            }
            break;
        default:
            std::cerr << "Invalid choice!" << std::endl;
            break;
    }

    return 0;
}









                                                          
                                                                              TASK 3

                                                                              TIC-TAC-TOE


#include <iostream>
#include <vector>


void displayBoard(const std::vector<std::vector<char>>& board) {
    std::cout << " " << board[0][0] << " | " << board[0][1] << " | " << board[0][2] << std::endl;
    std::cout << "---+---+---" << std::endl;
    std::cout << " " << board[1][0] << " | " << board[1][1] << " | " << board[1][2] << std::endl;
    std::cout << "---+---+---" << std::endl;
    std::cout << " " << board[2][0] << " | " << board[2][1] << " | " << board[2][2] << std::endl;
}


bool checkWin(const std::vector<std::vector<char>>& board, char player) {
    // Check rows
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player) {
            return true;
        }
    }
   
    for (int i = 0; i < 3; i++) {
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player) {
            return true;
        }
    }
    
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) {
        return true;
    }
    return false;
}


bool checkDraw(const std::vector<std::vector<char>>& board) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == '-') {
                return false;
            }
        }
    }
    return true;
}

int main() {
    std::vector<std::vector<char>> board = {{'-', '-', '-'}, {'-', '-', '-'}, {'-', '-', '-'}};
    char currentPlayer = 'X';

    while (true) {
        
        displayBoard(board);

       
        int row, col;
        std::cout << "Player " << currentPlayer << ", enter your move (row and column): ";
        std::cin >> row >> col;

        // Update the game board with the player's move
        if (row < 1 || row > 3 || col < 1 || col > 3) {
            std::cout << "Invalid move! Try again." << std::endl;
            continue;
        }
        if (board[row - 1][col - 1] != '-') {
            std::cout << "Cell already occupied! Try again." << std::endl;
            continue;
        }
        board[row - 1][col - 1] = currentPlayer;

       
        if (checkWin(board, currentPlayer)) {
            displayBoard(board);
            std::cout << "Player " << currentPlayer << " wins!" << std::endl;
            break;
        }

        
        if (checkDraw(board)) {
            displayBoard(board);
            std::cout << "It's a draw!" << std::endl;
            break;
        }

        
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

   
    char playAgain;
    std::cout << "Do you want to play again? (y/n): ";
    std::cin >> playAgain;
    if (playAgain == 'y') {
        main();
    }

    return 0;
}
                                                                            

                                                                                                     



                                                                        TASK 4 
                                                                    TO - DO - LIST 


#include <iostream>
#include <vector>
#include <string>


struct Task {
    std::string description;
    bool completed;
};


void addTask(std::vector<Task>& tasks) {
    Task task;
    std::cout << "Enter task description: ";
    std::getline(std::cin, task.description);
    task.completed = false;
    tasks.push_back(task);
    std::cout << "Task added successfully!" << std::endl;
}


void viewTasks(const std::vector<Task>& tasks) {
    std::cout << "To-Do List:" << std::endl;
    for (int i = 0; i < tasks.size(); i++) {
        std::cout << "[" << (i + 1) << "] " << tasks[i].description;
        if (tasks[i].completed) {
            std::cout << " (Completed)" << std::endl;
        } else {
            std::cout << " (Pending)" << std::endl;
        }
    }
}


void markTaskAsCompleted(std::vector<Task>& tasks) {
    int taskNumber;
    std::cout << "Enter the task number to mark as completed: ";
    std::cin >> taskNumber;
    if (taskNumber > 0 && taskNumber <= tasks.size()) {
        tasks[taskNumber - 1].completed = true;
        std::cout << "Task marked as completed!" << std::endl;
    } else {
        std::cout << "Invalid task number!" << std::endl;
    }
}


void removeTask(std::vector<Task>& tasks) {
    int taskNumber;
    std::cout << "Enter the number of task to remove: ";
    std::cin >> taskNumber;
    if (taskNumber > 0 && taskNumber <= tasks.size()) {
        tasks.erase(tasks.begin() + taskNumber - 1);
        std::cout << "Task removed successfully!" << std::endl;
    } else {
        std::cout << "Invalid task number!" << std::endl;
    }
}

int main() {
    std::vector<Task> tasks;

    while (true) {
        std::cout << "To-Do List Manager" << std::endl;
        std::cout << "-----------------" << std::endl;
        std::cout << "1. Add Task" << std::endl;
        std::cout << "2. View Tasks" << std::endl;
        std::cout << "3. Mark Task as Completed" << std::endl;
        std::cout << "4. Remove Task" << std::endl;
        std::cout << "5. Exit" << std::endl;
        std::cout << "Enter your choice: ";

        int choice;
        std::cin >> choice;

        switch (choice) {
            case 1:
                addTask(tasks);
                break;
            case 2:
                viewTasks(tasks);
                break;
            case 3:
                markTaskAsCompleted(tasks);
                break;
            case 4:
                removeTask(tasks);
                break;
            case 5:
                std::cout << "Goodbye!" << std::endl;
                return 0;
            default:
                std::cout << "Invalid choice!" << std::endl;
                break;
        }
    }

    return 0;
}   






                                                                          TASK 5 
                                                                    LIBRARY MANAGEMENT SYSTEM 




#include <iostream>
#include <vector>
#include <string>
#include <algorithm>
#include <ctime>

using namespace std;

class Book {
public:
    int id;
    string title;
    string author;
    string isbn;
    bool available;

    Book(int id, string title, string author, string isbn) : id(id), title(title), author(author), isbn(isbn), available(true) {}
};

class Borrower {
public:
    int id;
    string name;
    string contactInfo;

    Borrower(int id, string name, string contactInfo) : id(id), name(name), contactInfo(contactInfo) {}
};

class Transaction {
public:
    int transactionId;
    int bookId;
    int borrowerId;
    time_t checkoutDate;
    time_t dueDate;
    time_t returnDate;
    double fine;

    Transaction(int transactionId, int bookId, int borrowerId, time_t checkoutDate, time_t dueDate)
        : transactionId(transactionId), bookId(bookId), borrowerId(borrowerId), checkoutDate(checkoutDate), dueDate(dueDate), returnDate(0), fine(0) {}
};

class Library {
private:
    vector<Book> books;
    vector<Borrower> borrowers;
    vector<Transaction> transactions;
    int nextBookId = 1;
    int nextBorrowerId = 1;
    int nextTransactionId = 1;
    const double finePerDay = 1.0; // Example fine rate

public:
    void addBook(string title, string author, string isbn) {
        books.emplace_back(nextBookId++, title, author, isbn);
    }

    void addBorrower(string name, string contactInfo) {
        borrowers.emplace_back(nextBorrowerId++, name, contactInfo);
    }

    void searchBook(string query) {
        for (const auto& book : books) {
            if (book.title.find(query) != string::npos || book.author.find(query) != string::npos || book.isbn.find(query) != string::npos) {
                cout << "ID: " << book.id << ", Title: " << book.title << ", Author: " << book.author << ", ISBN: " << book.isbn << ", Available: " << (book.available ? "Yes" : "No") << endl;
            }
        }
    }

    void checkoutBook(int bookId, int borrowerId) {
        for (auto& book : books) {
            if (book.id == bookId && book.available) {
                time_t now = time(0);
                time_t dueDate = now + (7 * 24 * 60 * 60); // 7 days from now
                transactions.emplace_back(nextTransactionId++, bookId, borrowerId, now, dueDate);
                book.available = false;
                cout << "Book checked out successfully." << endl;
                return;
            }
        }
        cout << "Book not available for checkout." << endl;
    }

    void returnBook(int bookId) {
        for (auto& transaction : transactions) {
            if (transaction.bookId == bookId && transaction.returnDate == 0) {
                time_t now = time(0);
                transaction.returnDate = now;
                double daysLate = difftime(now, transaction.dueDate) / (24 * 60 * 60);
                if (daysLate > 0) {
                    transaction.fine = daysLate * finePerDay;
                }
                for (auto& book : books) {
                    if (book.id == bookId) {
                        book.available = true;
                        break;
                    }
                }
                cout << "Book returned successfully. Fine: $" << transaction.fine << endl;
                return;
            }
        }
        cout << "Transaction not found." << endl;
    }
};

void showMenu() {
    cout << "Library Management System" << endl;
    cout << "1. Add Book" << endl;
    cout << "2. Add Borrower" << endl;
    cout << "3. Search Book" << endl;
    cout << "4. Checkout Book" << endl;
    cout << "5. Return Book" << endl;
    cout << "6. Exit" << endl;
}

int main() {
    Library library;
    int choice;

    do {
        showMenu();
        cin >> choice;
        cin.ignore();
        switch (choice) {
            case 1: {
                string title, author, isbn;
                cout << "Enter title: ";
                getline(cin, title);
                cout << "Enter author: ";
                getline(cin, author);
                cout << "Enter ISBN: ";
                getline(cin, isbn);
                library.addBook(title, author, isbn);
                break;
            }
            case 2: {
                string name, contactInfo;
                cout << "Enter name: ";
                getline(cin, name);
                cout << "Enter contact info: ";
                getline(cin, contactInfo);
                library.addBorrower(name, contactInfo);
                break;
            }
            case 3: {
                string query;
                cout << "Enter search query (title/author/ISBN): ";
                getline(cin, query);
                library.searchBook(query);
                break;
            }
            case 4: {
                int bookId, borrowerId;
                cout << "Enter book ID: ";
                cin >> bookId;
                cout << "Enter borrower ID: ";
                cin >> borrowerId;
                library.checkoutBook(bookId, borrowerId);
                break;
            }
            case 5: {
                int bookId;
                cout << "Enter book ID: ";
                cin >> bookId;
                library.returnBook(bookId);
                break;
            }
            case 6:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 6);

    return 0;
}







                                                                         




