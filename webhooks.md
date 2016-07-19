# PayrollHero Webhooks

PayrollHero has a webhook system available to notify about various events in an employee's lifecycle.

## Data Objects

The Webhook Interface makes use of standardized payload objects to make sure that the responses are easily handled.

These are:

### Employee Object

```json
{
    "id": 1,
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
    "clock_in_time": "2016-07-15T19:28:25Z",
    "clock_out_time": "2016-07-15T19:28:25Z",
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
    "time": "2016-07-15T19:28:25Z",
    "shift": {}, # Shift Object, can be null
    "offsite": false,
    "unscheduled": false,
    "longitude": 1.23456, # can be null
    "latitude": 1.2345, # can be null
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


### `shift_reminder`

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


### `clocking`

**Fired When**:

Employee generates a clocking event of any kind (clock in/out break in/out)

**Payload**:

 * `account`: [Account Object](#account-object)
 * `employee`: [Employee Object](#employee-object)
 * `clocking`: [Clocking Object](#clocking-object)
