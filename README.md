# UI Lab 1
## Результат
<img src="https://github.com/ppc-ntu-khpi/35-tui-1-Dobrynya69/blob/master/result.png">

## Метод ShowCustomerDetails

``` java
private void ShowCustomerDetails() {
        TWindow custWin = addWindow("Customer Window", 2, 1, 40, 10, TWindow.NOZOOMBOX);
        custWin.newStatusBar("Enter valid customer number and press Show...");

        custWin.addLabel("Enter customer number: ", 2, 2);
        TField custNo = custWin.addField(24, 2, 3, false);
        TText details = custWin.addText("Owner Name: \nAccount Type: \nAccount Balance: ", 2, 4, 38, 8);
        custWin.addButton("&Show", 28, 2, new TAction() {
            @Override
            public void DO() {
                try {
                    int custNum = Integer.parseInt(custNo.getText());
                    Customer customer = Bank.getCustomer(custNum);
                    Account account = customer.getAccount(0);
                    String accountType = "";
                    if (account instanceof CheckingAccount){
                        accountType = "Checking";
                    } else if (customer.getAccount(0) instanceof SavingsAccount) {
                        accountType = "Savings";
                    } else{
                        accountType = "None";
                    }
                    details.setText("Owner Name: "+customer.getFirstName()+" (id="+custNum+")\nAccount Type: "+accountType+"\nAccount Balance: $"+account.getBalance()+"");
                } catch (Exception e) {
                    messageBox("Error", "You must provide a valid customer number!").show();
                }
            }
        });
    }
```
## Метод main

``` java
public static void main(String[] args) throws Exception {
        TUIdemo tdemo = new TUIdemo();
        DataSource data = new DataSource("C:/Users/roma0/Desktop/For the lessons/code/35-tui-1-Dobrynya69/data/test.dat");
        data.loadData();
        (new Thread(tdemo)).start();
    }
```
