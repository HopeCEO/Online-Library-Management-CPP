#include "User.h"
#include <sstream>
#include <algorithm>

User::User(const std::string& u, const std::string& n)
    : username(u), fullName(n) {}

std::string User::getUsername() const { return username; }
std::string User::getFullName() const { return fullName; }

bool User::borrowBook(const std::string& isbn) {
    // Optional: you can limit max books here (e.g. 5)
    // if (borrowedISBNs.size() >= 5) return false;

    borrowedISBNs.push_back(isbn);
    return true;
}

bool User::returnBook(const std::string& isbn) {
    auto it = std::find(borrowedISBNs.begin(), borrowedISBNs.end(), isbn);
    if (it == borrowedISBNs.end()) return false;
    borrowedISBNs.erase(it);
    return true;
}

const std::vector<std::string>& User::getBorrowedISBNs() const {
    return borrowedISBNs;
}

bool User::hasBorrowed(const std::string& isbn) const {
    return std::find(borrowedISBNs.begin(), borrowedISBNs.end(), isbn) != borrowedISBNs.end();
}

std::string User::toString() const {
    std::ostringstream oss;
    oss << username << " (" << fullName << ")  -  Books borrowed: " << borrowedISBNs.size();
    return oss.str();
}
