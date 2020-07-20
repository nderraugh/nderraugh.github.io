package com.company;

import java.util.HashSet;
import java.util.Set;

public class Main {

    private Set<String> set = new HashSet<String>();

    public void main(String[] args) {
        this.set.add("hello");
    }

    public String getFromStream() {
        return this.set.stream().findFirst().get();
    }

    public String getFromArray() {
        return this.set.toArray(new String[0])[0];
    }

    public String getFromIter() {
        return this.set.iterator().next();
    }

}
