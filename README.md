## Data Transfer Object (DTO) & Interfaces

#### Create module, controller and service
```bash
nest g module customer
```
```bash
nest g controller customer
```
```bash
nest g service customer
```
---


#### Create dto & interfaces folder
> <img width="368" height="182" alt="image" src="https://github.com/user-attachments/assets/ac36a273-2661-483c-b0ed-03ab2c7aed4e" />

> <img width="375" height="89" alt="image" src="https://github.com/user-attachments/assets/53823910-f4c1-4422-8467-1938a6540d8b" />

### `customer.interface.ts`
```bash
export interface Customer{
    id: number;
    name: string;
    age: number;
}
```
---

### `create-customer.dto.ts`
```bash
export class CreateCustomerDto {
    name: string;
    age: number;
}
```
---


### `customer.service.ts`
```bash
import { Injectable } from '@nestjs/common';
import { Customer } from './interfaces/customer.interface';
import { CreateCustomerDto } from './dto/create-customer.dto';

@Injectable()
export class CustomerService {
    private customers: Customer[] = [];

    getAllCustomers(): Customer[] {
        return this.customers;
    }

    addCustomer(createCustomerDto: CreateCustomerDto): Customer {
        const newCustomer: Customer = {
            id: Date.now(),
            ...createCustomerDto
        };
        this.customers.push(newCustomer);
        return newCustomer;
    }

}
```
---














