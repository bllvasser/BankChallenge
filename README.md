# BankChallenge
package com.company;

import java.util.ArrayList;

public class Customer {

    private String name;
    private ArrayList<Double> myTransactions;


    public Customer(String name) {
        this.name = name;
        this.myTransactions = new ArrayList<>();
    }

    public void addTransaction(double amt) {
        this.myTransactions.add(amt);
    }

    public String getName() {
        return name;
    }

    public ArrayList<Double> getTransactions() {
        return myTransactions;
    }

    public static Customer createCustomer(String name) {
        return new Customer(name);
    }


}
package com.company;

import java.beans.Customizer;
import java.util.ArrayList;


public class Branch {
    private ArrayList<Customer> myCustomer;
    private ArrayList<Double> myTransactions;
    private String branch;
    private String name;


    public Branch(String name) {

        this.myCustomer = new ArrayList<Customer>();
        this.myTransactions = new ArrayList<Double>();
        this.branch = branch;
        this.name = name;

    }

    public String getName() {
        return name;
    }

    public static Branch createBranch(String name) {
        return new Branch(name);
    }

    public String getBranch() {
        return branch;
    }

    public ArrayList<Customer> getCustomers() {
        return myCustomer;
    }

    public boolean addNewCustomer(Customer customer) {
        if (findCustomer(customer.getName()) >= 0) {
            System.out.println("Customer is not on file");
            return false;
        }

        myCustomer.add(customer);
        return true;
    }

    private int findCustomer(Customer customer) {

        return this.myCustomer.indexOf(customer);
    }

    private int findCustomer(String customerName) {
        for (int i = 0; i < this.myCustomer.size(); i++) {
            Customer customer = this.myCustomer.get(i);
            if (customer.getName().equals(customerName)) {
                return i;
            }
        }
        return -1;
    }

    public boolean addNewTransaction(String custName, double amt) {
        Customer existCust = findCust(custName);
        if (existCust != null) {
            existCust.addTransaction(amt);
            return true;
        }

        return false;
    }

    private Customer findCust(String custName) {
        for (int i = 0; i < this.myCustomer.size(); i++) {
            Customer checkedCust = this.myCustomer.get(i);
            return checkedCust;
        }
        return null;
    }


}

package com.company;

import java.util.ArrayList;


public class Bank {
    // private ArrayList<Double> myTransactions;
    private ArrayList<Branch> myBranch;
    private ArrayList<Customer> myCustomer;


    public Bank() {
        this.myBranch = new ArrayList<Branch>();
        this.myCustomer = new ArrayList<Customer>();
        //   this.myTransactions = new ArrayList<Double>();
    }

    Branch branch = new Branch("yowsey");


    public boolean printCustomerList(String branchName, boolean showtran) {
        Branch branch = findBranch(branchName);
        if (branch != null) {
            System.out.println("Customer details for branch " + branch.getName());

            ArrayList<Customer> branchCust = branch.getCustomers();
            for (int i = 0; i < branchCust.size(); i++) {
                Customer branchCusto = branchCust.get(i);
                System.out.println("Customer: " + branchCusto.getName() + " [ " + (i + 1) + "]");
                if (showtran) {
                    System.out.println("Transactions");
                    ArrayList<Double> transactions = branchCusto.getTransactions();
                    for (int j = 0; j < transactions.size(); j++) {
                        System.out.println(" [ " + (j + 1) + " ] Amount " + transactions.get(j));
                    }
                }
            }
            return true;
        } else {
            return false;
        }

    }

    public boolean addNewBranch(Branch branch) {
        if (findBranch(branch.getBranch()) != branch) {
            System.out.println("Branch is not on file");
            return false;
        }

        myBranch.add(branch);
        return true;
    }

    private int findBranch(Branch branch) {

        return this.myBranch.indexOf(branch);
    }

    private Branch findBranch(String branchName) {
        for (int i = 0; i < this.myBranch.size(); i++) {
            Branch checkedBranch = this.myBranch.get(i);
            if (checkedBranch.getName().equals(branchName)) {
                return checkedBranch;
            }
        }
        return null;
    }

    public boolean addNewCustomer(Customer customer) {
        if (findCustomer(customer.getName()) >= 0) {
            System.out.println("Customer is not on file");
            return false;
        }

        myCustomer.add(customer);
        return true;
    }

    private int findCustomer(Customer customer) {

        return this.myCustomer.indexOf(customer);
    }

    private int findCustomer(String customerName) {
        for (int i = 0; i < this.myCustomer.size(); i++) {
            Customer customer = this.myCustomer.get(i);
            if (customer.getName().equals(customerName)) {
                return i;
            }
        }
        return -1;
    }

    public void addNewTransaction(String name, double amt) {

        branch.addNewTransaction(name, amt);
    }


}

package com.company;

import java.util.ArrayList;
import java.util.Scanner;

public class Main {


    private static Scanner scanner = new Scanner(System.in);
    private static Bank bank = new Bank();
    private static Customer customer = new Customer("Yowsey");
    private static Branch branch = new Branch("yowsey");
    private static ArrayList<Double> myTransactions = new ArrayList<Double>();

    public static void main(String[] args) {


        boolean quit = false;
        printActions();

        while (!quit) {
            System.out.println("\nEnter action: (6 to show available actions)");
            int action = scanner.nextInt();

            switch (action) {
                case 1:
                    System.out.println("\n shutting down...");
                    break;

                case 2:
                    bank.printCustomerList("branchName", true);
                    break;

                case 3:
                    addNewCustomer();

                case 4:
                    addNewBranch();
                    break;

                case 5:
                    addNewTransaction("yowsey", 0.0);
                    break;

                case 6:
                    printActions();
                    break;
            }
        }

    }

    private static void printActions() {
        System.out.println("\n Available actions: \n press");
        System.out.println("1 - to shutdown\n " +
                "2 - to print customer list\n " +
                "3 - to add a new customer\n " +
                "4 - to add a new branch\n " +
                "5 - to add a new transaction\n " +
                "6 - to print a list of available actions.");
        System.out.println("Choose your action: ");
    }

    private static void addNewCustomer() {
        System.out.println("Enter customer name");
        String name = scanner.nextLine();
        System.out.println("Enter transaction amount");
        String tranAmt = scanner.nextLine();
        Customer newCustomer = Customer.createCustomer(name);
        if (bank.addNewCustomer(newCustomer)) {
            System.out.println("New customer added: name " + name + ", transaction amount = " + tranAmt);
        }
    }

    private static void addNewBranch() {
        System.out.println("Enter branch name");
        String name = scanner.nextLine();
        Branch newBranch = Branch.createBranch(name);
        if (bank.addNewBranch(newBranch)) {
            System.out.println("New branch added: name " + name);
        }
    }

    private static void addNewTransaction(String name, double amt) {
        System.out.println("Enter transaction amount");
        double tranamt = scanner.nextDouble();
        bank.addNewTransaction(name, amt);
    }
}



