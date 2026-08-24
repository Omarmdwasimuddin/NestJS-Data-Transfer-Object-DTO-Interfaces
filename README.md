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


### `customer.controller.ts`
```bash
import { Body, Controller, Get, Post } from '@nestjs/common';
import { CustomerService } from './customer.service';
import { CreateCustomerDto } from './dto/create-customer.dto';

@Controller('customer')
export class CustomerController {
    constructor(private readonly customerService: CustomerService) {};

    @Get()
    getCustomers(){
        return this.customerService.getAllCustomers();
    }

    @Post()
    addCustomer(@Body() createCustomerDto: CreateCustomerDto) {
        return this.customerService.addCustomer(createCustomerDto);
    }

}
```
---
> ## OUTPUT
> GET
>
> <img width="862" height="685" alt="image" src="https://github.com/user-attachments/assets/8692003d-4d82-4199-bae9-b7d4752c7ebe" />
>
> ---
> POST
> 
> <img width="868" height="546" alt="image" src="https://github.com/user-attachments/assets/ca4d4f8e-050b-4168-b464-2f2d59becfc6" />
















