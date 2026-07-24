# Insurance Policy Management System

A comprehensive Python-based policy management system for insurance companies. This system manages policyholders, insurance products, and payment processing with features for registration, suspension, reactivation, and payment management.

## Features

### Policyholder Management
- **Register new policyholders** with personal information
- **Suspend policies** for non-payment or other reasons
- **Reactivate suspended policies**
- **Track policy products** registered to each policyholder
- **View account details** including all registered products and payment history

### Product Management
- **Create insurance products** with premiums and coverage details
- **Update premiums** dynamically
- **Modify coverage amounts** for existing products
- **Suspend/Reactivate products** from new registrations
- **Categorized products** (Life, Health, Car, Home Insurance)

### Payment Processing
- **Process payments** for policy products
- **Track payment status** (Pending, Completed, Overdue, Failed)
- **Automatic penalty calculation** for overdue payments (5% penalty)
- **Send payment reminders** before due dates (5 days default)
- **Check overdue status** with automatic penalty application
- **Maintain payment history** for each policyholder

## Project Structure

```
policy-management-system/
├── policyholder.py       # Policyholder class and status management
├── product.py            # Insurance product class and management
├── payment.py            # Payment processing and tracking
├── main.py              # Demonstration and testing
└── README.md            # This file
```

## Installation

1. **Clone or download the repository**:
   ```bash
   git clone https://github.com/yourusername/policy-management-system.git
   cd policy-management-system
   ```

2. **Ensure you have Python 3.7+** installed:
   ```bash
   python --version
   ```

3. **No external dependencies required** - Uses only Python standard library

## Usage

### Running the Demonstration

Execute the main script to see a complete demonstration of the system:

```bash
python main.py
```

This will:
1. Create three insurance products (Health, Car, Life)
2. Register two policyholders
3. Register products for each policyholder
4. Process multiple payments
5. Display account details
6. Demonstrate suspension/reactivation
7. Show payment transaction details

### Using the Classes Independently

#### Creating a Policyholder

```python
from policyholder import Policyholder

# Create a new policyholder
ph = Policyholder(
    name="John Doe",
    email="john@email.com",
    phone="555-1234",
    address="123 Main St"
)

# Check status
print(ph.status.value)  # "active"

# Suspend the policy
ph.suspend(reason="Non-payment")

# Reactivate the policy
ph.reactivate()
```

#### Creating and Managing Products

```python
from product import Product, ProductType

# Create a product
product = Product(
    product_name="Premium Health Insurance",
    product_type=ProductType.HEALTH_INSURANCE,
    premium=150.00,
    coverage_amount=100000.00,
    description="Comprehensive health coverage"
)

# Update premium
product.update_premium(175.00)

# Update coverage
product.update_coverage(150000.00)

# Suspend product
product.suspend()

# Reactivate product
product.reactivate()

# Get product details
details = product.get_product_details()
print(details)
```

#### Processing Payments

```python
from payment import Payment
from datetime import datetime, timedelta

# Create a payment
payment = Payment(
    policyholder=ph,
    product=product,
    amount=150.00,
    due_date=datetime.now() + timedelta(days=30)
)

# Check if overdue
payment.check_overdue()

# Send reminder
payment.send_payment_reminder()

# Process payment
payment.process_payment()

# Apply penalty if overdue
total_due = payment.apply_penalty()

# Get payment details
details = payment.get_payment_details()
print(details)
```

#### Registering Products to Policyholders

```python
# Register a product for a policyholder
success = policyholder.register_product(product)

# View account details
details = policyholder.get_account_details()
print(details)
```

## Class Reference

### Policyholder

Manages individual policyholders and their registered products.

**Key Methods:**
- `register_product(product)` - Register a product for this policyholder
- `suspend(reason)` - Suspend the policyholder's policy
- `reactivate()` - Reactivate a suspended policy
- `add_payment_record(payment_record)` - Record a payment
- `get_account_details()` - Get complete account information

**Attributes:**
- `policyholder_id` - Unique identifier
- `name` - Full name
- `email` - Email address
- `phone` - Phone number
- `address` - Physical address
- `status` - Current status (Active/Suspended/Inactive)
- `products` - Dictionary of registered products
- `payment_history` - List of payment records

### Product

Represents an insurance product offering.

**Key Methods:**
- `update_premium(new_premium)` - Update the monthly premium
- `update_coverage(new_coverage)` - Update coverage amount
- `suspend()` - Suspend the product from new registrations
- `reactivate()` - Reactivate a suspended product
- `get_product_details()` - Get complete product information

**Attributes:**
- `product_id` - Unique identifier
- `product_name` - Name of the product
- `product_type` - Type of insurance (Life, Health, Car, Home)
- `premium` - Monthly premium amount
- `coverage_amount` - Maximum coverage provided
- `active` - Whether the product is available

### Payment

Handles payment processing and tracking.

**Key Methods:**
- `process_payment()` - Process the payment transaction
- `check_overdue()` - Check if payment is overdue
- `send_payment_reminder()` - Send reminder if due soon
- `apply_penalty()` - Apply penalty to overdue payment
- `get_payment_details()` - Get complete payment information

**Attributes:**
- `transaction_id` - Unique transaction identifier
- `amount` - Payment amount
- `status` - Current status (Pending/Completed/Overdue/Failed)
- `due_date` - When payment is due
- `payment_date` - When payment was made
- `penalty_amount` - Applied penalty amount

## Key Features Explained

### Automatic ID Generation

Each class (Policyholder, Product, Payment) generates unique IDs automatically:
- **Policyholders**: `PH1001`, `PH1002`, etc.
- **Products**: `PRD5001`, `PRD5002`, etc.
- **Payments**: `TXN9001`, `TXN9002`, etc.

### Payment Management

- **Overdue Detection**: Automatically identifies and tracks overdue payments
- **Penalty System**: Applies 5% penalty on overdue amounts
- **Reminders**: Sends reminders 5 days before due date
- **Payment History**: Maintains complete transaction record for each policyholder

### Status Tracking

- **Policyholders**: Active, Suspended, Inactive
- **Products**: Active, Suspended
- **Payments**: Pending, Completed, Overdue, Failed

## Example Output

When you run `python main.py`, you'll see:

```
======================================================================
 INSURANCE POLICY MANAGEMENT SYSTEM
======================================================================

[Step 1: Creating Insurance Products]
✓ Created: Product(ID=PRD5001, Name=Premium Health Insurance, Premium=$150.00, Status=Active)
✓ Created: Product(ID=PRD5002, Name=Comprehensive Car Insurance, Premium=$120.00, Status=Active)
✓ Created: Product(ID=PRD5003, Name=Life Insurance Plus, Premium=$200.00, Status=Active)

======================================================================
 CREATING POLICYHOLDERS
======================================================================

✓ Created: Policyholder(ID=PH1001, Name=John Smith, Status=active)
✓ Created: Policyholder(ID=PH1002, Name=Sarah Johnson, Status=active)

[Registering products for John Smith]
Product 'Premium Health Insurance' registered for John Smith.
Product 'Comprehensive Car Insurance' registered for John Smith.

...more output...
```

## Data Validation

The system includes validation for:
- Premium and coverage amounts must be greater than zero
- Duplicate product registrations are prevented
- Suspended policyholders cannot register new products
- Payment amounts must be positive
- Suspension/reactivation checks prevent redundant operations

## Error Handling

All methods include appropriate error handling and user feedback:
- Invalid inputs are rejected with informative messages
- Status checks prevent invalid operations
- Transaction success/failure is clearly reported

## Future Enhancements

Potential improvements for future versions:
- Database integration (SQLite, PostgreSQL)
- User authentication and authorization
- Email notifications for payment reminders
- Automated policy renewal system
- Claims processing module
- Commission calculation for agents
- Advanced reporting and analytics
- Web interface (Flask/Django)
- REST API for external integration


---

**Version**: 1.0  
**Last Updated**: 2026-07-24  
**Author**: Insurance Management Team
