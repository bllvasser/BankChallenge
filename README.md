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
