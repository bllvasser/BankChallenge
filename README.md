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


