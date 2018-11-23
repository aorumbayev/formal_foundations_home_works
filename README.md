<p align="center"><img width=80% src="assets/logo.png"></p>

## Algebraic specifications of ATM

Solution of HW1 for NTIN043 course.

### How-to

In order to execute the module simply provide the `.maude` file as an argument to maude executable. All `rew` statements for test cases are going to be executed automatically. The usage of `print attribute` also allows to see logs from execution of specific rules inside various modules.

```
$ {maude executable} atm-specs.maude
```

### Solution overview

Solution in `atm-specs.maude` consist of several modules and functional modules described below.

---

#### Bank Database, Account and Pin verification and storage.

• `BANK_DATABASE{K :: TRIV, V :: TRIV}` - An implementation of a database used by a Bank that has a `protecting` `MAP` field. Defines specification using rules on how to store the `AccountId` and `Pin` idenfitied by `String` and `Int` inside the map.
• `BANK_DATABASE_TEST` - A module used for executing test cases for the bank database. Default configuration supports adding an account and checking wheter the account inside the database and the pin entered by user is corresponding to the pin stored in database for that particular `AccountId`.

---

#### Bank account, trivial withdraw, deposit and transfer operations.

• `BANK_ACCOUNT` - A module used for specification of BankAccount that supports main operations on `deposit`, `withdraw` and `transfer` using mixfix notation. The `withdraw` is defined by a conditional rule that also checks that the rule is being rewritten only if the User has enought balance on his account.
• `BANK_ACCOUNT_TEST` - A module used for executing test cases for the bank database. Default configuration demonstrate the series of `deposit`, `withdraw` and `transfer` operations perfomed on two different bank accounts.

---

#### ATM, withdraw and deposit operations based on amount of banknotes available.

• `ATM` - A module used for specifications of the ATM unit. Each banknote is represented as a state. Two main rules named `processDepositRequest` and `processWithdrawRequest` are accepting the `Msg` describing the `ATM` and `BANK_ACCOUNT`. Depending on the amount of available banknotes in `ATM` the corresponding amount will be either deposited or withdrawn using rules specified in `BANK_ACCOUNT`. Similar to `withdraw` in `BANK_ACCOUNT` module, `ATM` module will only perform `processWithdrawRequest` if the `ATM` has sufficient amount of specified banknotes otherwise it will not proceed with operation.
