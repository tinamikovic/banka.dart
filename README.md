
 class IBank {
// sučelje
  double getBalance();
  void deposit(amount);
  void withdraw(amount);
}

 class Transaction {
// sučelje
  double get amount;
  DateTime get date;
  void execute(IBank bank);
}


 class Person {
// Apstrakcija
  String get firstName;
  String get lastName;
  String get address;
  IBank get bankAccount; 


class User implements Person, IBank {
  final String firstName;
  final String lastName;
  final String address;
  final IBank bankAccount;

  User(this.firstName, this.lastName, this.address, this.bankAccount);

  @override
  double getBalance() => bankAccount.getBalance();

  @override
  void deposit(double amount) => bankAccount.deposit(amount);

  @override
  void withdraw(double amount) => bankAccount.withdraw(amount);

  @override
  String get firstName => this.firstName;

  @override
  String get lastName => this.lastName;

  @override
  String get address => this.address;

  @override
  IBank get bankAccount => this.bankAccount;
}

class BankAccount implements IBank {
  double _balance = 0.0;

  @override
  double getBalance() => _balance;

  @override
  void deposit(double amount) {
    if (amount > 0) {
      _balance += amount;
    } else {
      throw Exception("Invalid deposit amount");
    }
  }

  @override
  void withdraw(double amount) {
    if (amount > 0 && amount <= _balance) {
      _balance -= amount;
    } else {
      throw Exception("Insufficient funds or invalid withdraw amount");
    }
  }
}

class Deposit implements Transaction {
  final double amount;
  final DateTime date;

  Deposit(this.amount, this.date);

  @override
  double get amount => this.amount;

  @override
  DateTime get date => this.date;

  @override
  void execute(IBank bank) => bank.deposit(amount);
}

class Withdrawal implements Transaction {
  final double amount;
  final DateTime date;

  Withdrawal(this.amount, this.date);

  @override
  double get amount => this.amount;

  @override
  DateTime get date => this.date;

  @override
  void execute(IBank bank) => bank.withdraw(amount);
}
