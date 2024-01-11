#include <iostream>
#include <string>
using namespace std;
struct Book {
    string title;
    string author;
    int publicationYear;
    string genre;
};

void inputDetails(Book books[], int size) {
    for (int i = 0; i < size; ++i) {
        cout << "Enter details for Book " << i + 1 << ":" << endl;
        cout << "Enter the title of the book : ";
        getline(cin, books[i].title);
        cout << "Enter author's name : ";
        getline(cin, books[i].author);
        cout << "Enter publication Year of the book: ";
        cin >> books[i].publicationYear;
        cin.ignore(), '\n';
        cout << "Enter the genre of the book: ";
        getline(cin, books[i].genre);
        cout << endl;
    }
}

void categorizeBooks(const Book books[], int size, Book fiction[], Book nonfiction[], int& fictionCount, int& nonfictionCount) {
    fictionCount = nonfictionCount = 0;

    for (int i = 0; i < size; ++i) {
        if (books[i].genre == "Fiction") {
            fiction[fictionCount++] = books[i];
        }
        else {
            nonfiction[nonfictionCount++] = books[i];
        }
    }
}
void findEarliestBook(const Book books[], int count, Book& earliestBook) {
    earliestBook = books[0];
    for (int i = 1; i < count; ++i) {
        if (books[i].publicationYear < earliestBook.publicationYear) {
            earliestBook = books[i];
        }
    }
}

void displayDetails(const Book fiction[], int fictionCount, const Book nonfiction[], int nonfictionCount,
    const Book& earliestFiction, const Book& earliestNonfiction) {
    cout << "Fiction Books:" << endl;
    for (int i = 0; i < fictionCount; ++i) {
        cout << "Title: " << fiction[i].title << ", Author: " << fiction[i].author << ", Publication Year: "
            << fiction[i].publicationYear << ", Genre: " << fiction[i].genre << endl;
    }
    cout << "Earliest fiction Book: " << earliestFiction.title << " by " << earliestFiction.author << endl;

    cout << "\nNon-Fiction Books:" << endl;
    for (int i = 0; i < nonfictionCount; ++i) {
        cout << "Title: " << nonfiction[i].title << ", Author: " << nonfiction[i].author << ", Publication Year: "
            << nonfiction[i].publicationYear << ", Genre: " << nonfiction[i].genre << endl;
    }
    cout << "Earliest non-fiction Book: " << earliestNonfiction.title << " by " << earliestNonfiction.author << endl;
}

int main() {
    const int size = 6;
    Book books[size];
    Book fiction[size], nonfiction[size];
    int fictionCount, nonfictionCount;
    Book earliestFiction, earliestNonfiction;

    inputDetails(books, size);
    categorizeBooks(books, size, fiction, nonfiction, fictionCount, nonfictionCount);
    findEarliestBook(fiction, fictionCount, earliestFiction);
    findEarliestBook(nonfiction, nonfictionCount, earliestNonfiction);
    displayDetails(fiction, fictionCount, nonfiction, nonfictionCount, earliestFiction, earliestNonfiction);

    return 0;
}
