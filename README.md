![Untitled](/piper-hat.png)

# Finhance Development Blueprint

## User Roles

1. Store Staff
2. Warehouse Incharge
3. Accounts
4. Management

**Store Staff Use-cases**

1. Issue transfer of goods statements
    1. Internal (from warehouse A to B) (STC)
    2. External (incoming stock or outgoing stock from third party) (GRN, GP)

**Store Staff User Profiling**

1. Stateless
2. Low-literate
3. Not very tech-savvy
4. No incentive to fill the form correctly → low attention to detail → frequent errors 
    1. Solution:
        1. View (only) last submission (1-time edit authority)
5. Small screen android devices which are **always-online** during office hours → (v2)
    1. For v1, assume PC or laptop
6. No modification rights
7. Single warehouse assigned

**Warehouse Incharge Use-cases / User Profiling**

1. Verify entries through physical bills (Challan, Invoice, Cashbook Number), have to input either Challan or Invoice mandated
2. Inputs a new field price (not mandatory)
3. Scope of error → low (put some sanity checks such as Total amount autofilled)
4. PC or laptop
5. Stateful (Viewing permission - History of goods from the concerned warehouse not the price)
6. Edit rights: Same date entries only, Neither back-date nor future date
7. Create/Modify/Delete Product
8. New Category

**Accounts Staff Use-cases**

1. Responsible for maintaining a separate account for every third-party
    1. For every invoice the Ground Staff issues, the account adds it to the account of the concerned third-party.
2. Fill all the prices in the invoice (mandatory), If Challan not mandatory
3. Sanity checks (Goods-level check such as Negative stock not allowed (Warning or Disable), mapping from invoice to goods flow statement)

**Accounts Staff User Profiling**

1. Literate
2. Scope of error is high but low in comparison to ground staff 
3. Typically use a PC or a laptop for their daily chores

**Analysis & Strategy Use-cases**

1. Verify invoices with transfer of goods statement
    1. For every invoice and their corresponding transfer of goods statement, check for consistency
2. Analyze the flow of goods and cash trend to generation actionable insights.

**Analysis & Strategy User Profiling**

1. Literate
2. Busy (generate tasks to be completed in small gaps of rest)
3. Operates on both laptop and phone

**************************Form Features**************************

- Narrow search drop-down
- Statefulness
- Show form summary before submitting
- Design a form primarily for PC
- Login extensible
- Form view role-based
- Form field validations (client-side, server-side)
- 

[react-google-forms-hooks](https://www.npmjs.com/package/react-google-forms-hooks)


**Created a Google Form to record entries**

1. Follow tutorial here: https://howtogapps.com/generate-invoices-using-google-form-and-sheets/
2. Form's [Mobile link](https://forms.gle/7nBqXiHWdrB7XWjQA)
3. Form's [PC Link](https://forms.gle/wN9zXKZ8kRwAwcgk9)

## Blog Series

### [1. Learn to publish Notion Pages on your website No-Code](/blog/blog1/content.md)

### 2. Use-case Driven Engineering (Coming Soon)


## Important Links

### Hacker News article on Ledger Engineering: https://news.ycombinator.com/item?id=36506782
### AWS QLDB: https://aws.amazon.com/blogs/industries/building-a-core-banking-system-with-amazon-quantum-ledger-database/
### Ledger Engineering Mistakes: https://www.andriosrobert.com/p/things-i-wish-i-knew-before-building
### Tutorial on Engineering practices: https://blog.journalize.io/posts/an-elegant-db-schema-for-double-entry-accounting/
### TigerBeetleDB: https://tigerbeetle.com
### Twisp: https://www.twisp.com