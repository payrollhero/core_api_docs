# PayrollHero Webhooks

PayrollHero has a webhook system available to notify about various events in an employee's lifecycle.

## Data Objects

The Webhook Interface makes use of standardized payload objects to make sure that the responses are easily handled.

These are:

### Employee Object

```json
{
    "id": 1,
    "account": {}, # Account Object
    "phone_numbers": [
      {
        "label": "main",
        "number": "+1 123-223-3343"
      }
    ],
    "fullname": "John Doe"
}
```

### Shift Object
```json
{
    "clock_in_time": "2016-07-15T19:28:25+00:00",
    "clock_out_time": "2016-07-15T19:28:25+00:00",
    "earliest_clock_in_time": "2016-07-15T19:28:25+00:00",
    "earliest_clock_out_time": "2016-07-15T19:28:25+00:00",
    "latest_clock_in_time": "2016-07-15T19:28:25+00:00",
    "latest_clock_out_time": "2016-07-15T19:28:25+00:00",
    "worksite": {} # Worksite Object
}
```

### Worksite Object
```json
{
    "id": 1,
    "name": "Office"
}
```

### Clocking Object
```json
{
    "kind": "clock_in",
    "time": "2016-07-15T19:28:25+00:00",
    "shift": {} || null, # Shift Object
    "worksite": {} || null, # Worksite Object
    "offsite": false,
    "unscheduled": false,
    "longitude": 1.23456 || null,
    "latitude": 1.2345 || null,
    "device": "MyClock 3.2 - iPhone 4,2",
    "ip": "1.2.3.4"
}
```

### Account Object

```json
{
    "id": 1,
    "name": "PayrollHero"
}
```

## Event Types

### `upcoming_shift`

**Fired When**:

When generating reminders for next shift, usually ~24h in advance of shift

Also when its re-generated due to schedule changes

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `shift`: [Shift Object](#shift-object)

### `shift_starting_soon`

**Fired When**:

~1h before earliest clock in of shift (rollcall reminder)

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `shift`: [Shift Object](#shift-object)

### `missed_clocking_in`

**Fired When**:

TBD

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `shift`: [Shift Object](#shift-object)

### `missed_clocking_out`

**Fired When**:

TBD

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `shift`: [Shift Object](#shift-object)

### `unscheduled_work`

**Fired When**:

Employee works an unscheduled shift

Fired on Clock in and on Clock Out

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `clocking`: [Clocking Object](#clocking-object)

### `offsite_work`

**Fired When**:

Employee works offsite

Fired any time an offsite clock in or clock out happens

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `clocking`: [Clocking Object](#clocking-object)

### `clocking`

**Fired When**:

Employee generates a clocking event of any kind (clock in/out break in/out)

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `clocking`: [Clocking Object](#clocking-object)
