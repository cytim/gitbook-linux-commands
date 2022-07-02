# Entity-attribute-value Model

> Entity–attribute–value model (EAV) is a data model to encode, in a space-efficient manner, entities where the number
> of attributes (properties, parameters) that can be used to describe them is potentially vast, but the number that will
> actually apply to a given entity is relatively modest.
>
> EAV is also known as _object–attribute–value model_, _vertical database model_, and _open schema_.
>
> \- [Wikipedia](https://en.wikipedia.org/wiki/Entity%E2%80%93attribute%E2%80%93value_model)

As an example, assume that we are building _a Know Your Customer (KYC) system_ and we have to design a database table to
store the identity information of a person.

During the KYC process, the person can submit any kind of identity documents for us to identify him, including the
national identity card, passport, driving license, residence permit and many more.

Each type of identity documents contains different information. If we have to design a database table to store all
possible attributes for all possible identity documents, the table will end up to have **dozens of columns** where most
of them will be **null for most of the records**.

Possible information on an identity document:

- Document Number
- Full Name
- First Name
- Last Name
- Date of Birth
- Gender
- Nationality
- Issuing Country
- Issuing Date
- Expiry Date
- Residential Address
- Marital Status
- Occupation
- (...)

Instead of including every possible attribute as the columns, we can design the table to follow the EAV model.

```sql
CREATE TABLE "identity_documents" (
  "cumtomer_id" bigint NOT NULL,
  "attribute" varchar(255) NOT NULL,
  "value" varchar(255) NOT NULL
);
```

As a result, different customers can have different set of `identity_documents` records.

| customer_id | attribute         | value                |
| ----------- | ----------------- | -------------------- |
| `42`        | `"full_name"`     | `"Satoshi Nakamoto"` |
| `42`        | `"date_of_birth"` | `"1975-04-05"`       |
| `42`        | `"nationality"`   | `"JPN"`              |
| `128`       | `"first_name"`    | `"Elon"`             |
| `128`       | `"middle_name"`   | `"Reeve"`            |
| `128`       | `"last_name"`     | `"Musk"`             |
| `128`       | `"date_of_birth"` | `"1971-06-28"`       |
| `128`       | `"occupation"`    | `"entrepreneur"`     |
