# Strategy

It is based on the principle of composition over inheritance. It defines a family of algorithms, encapsulates each one, and makes them interchangeable at runtime. The core idea behind this pattern is to separate the algorithms from the main object. This allows the object to delegate the algorithm's behavior to one of its contained strategies.



![Screenshot 2023-05-05 at 13.47.33.png](./attachments/Screenshot%202023-05-05%20at%2013.47.33.png)
```typescript 
interface IStrategy {
  calculate(amount: number): number;
}

class SaleContext {
  constructor(private strategy: IStrategy) {}
  
  calculate(amount) {
    return this.strategy.calculate(amount);
  }
  
  setStrategy(strategy: IStrategy) {
    this.strategy = strategy;
  }
}


// Strategies
class RegularSaleStrategy {
  constructor(private tax: number) {}
  
  calculate(amount: number): number {
    return amount + (amount * this.tax);
  }
}

class DiscountSaleStrategy {
  constructor(private tax: number, private discount: number) {}
  
  calculate(amount: number): number {
    return amount + (amount * this.tax) - this.discount;
  }
}

class ForeignSaleStrategy {
  calculate(amount: number): number {
    return amount * this.getDollarPrice();
  }
  
  getDollarPrice() {
  // here we could make a call to an API to get that information
    return 20;
  }
}

const regularSale = new RegularSaleStrategy(0.16);
const discountSale = new DiscountSaleStrategy(0.16, 20);
foreignSale = new ForeignSaleStrategy();

const sale = new SaleContext(regularSale);

// regular sale
sale.calculate(120);
// output: 139.2

// discount sale
sale.setStrategy(discountSale);
sale.calculate(120);
// output: 119.2

// foreign sale
sale.setStrategy(foreignSale);
sale.calculate(120);
// output: 2400
```
