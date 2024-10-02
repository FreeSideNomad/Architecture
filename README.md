# TransactR Architecture

## Domain Model

![Domain Model](https://github.com/FreeSideNomad/Architecture/blob/main/TransactR-Domain%20model.png)

At its core TransactR domain is concerned with maintaining set of customers that have accounts. Accounts have balances and transactions. 

For example:

Customer ABC Holdings has a Saving Account.
Saving Account has current balance of $150.00 and following transactions:

```
Date        Transaction Type  Amount   Current Balance
1  Jan 2024 Deposit             $100              $100
1  Feb 2024 Interest              $5              $105 
15 Feb 2024 Deposit              $80              $185
1  Mar 2024 Interest              $6              $191
15 Mar 2024 Withdrawal           $41              $150
```

From this we can see that for Savings Account Type we can define 3 transaction types (Deposit, Interest and Withdrawal), 1 balance type (Current Balance)
and that Deposit and Interest credit Current Balance (increase value) and Withdrawal debits current balance (decreases value)

Tenant is typically a business entity that owns either configuration such as Account Types (System Tenant) or configuration and customer and account data.

Tenants are hierarchical, so for example head office of the company can be a parent tenant and subsidiaries/ branches can be subtenant.

Root tenant is TransactR and it can have subtenants such as Loans, Deposits, Subscriptions. This allows certain types of accounts to be defined on the top levels of the 
hierachy and inherited by lower levels.

Each tenant has users which can see customers and accounts for that tenant and any subtenants. Opposite is not true (child cannot see customers and accounts of the parent)

## Logical Architecture

![Logical Architecture](https://github.com/FreeSideNomad/Architecture/blob/main/Transact%20R%20Logical%20view.png)

System stores all of its data in SQL Server. Application is written in Java.

Each tenant can enter data about their clients (accounts, transactions) through Admin UI.

On other hand each tenant can have their own web application that is exposed to their customers. For example if tenant was offering savings accounts, their clients will be able to login to their 
online portal that will allow them to see the balances and transactions and initiate deposits and withdrawals. Data for this online portal is exposed though Client API.
