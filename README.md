from datetime import datetime


class Customer:
    """Class representing a customer with contact details, loyalty membership, and a shopping cart."""

    def __init__(self, name, contact_info, is_loyalty_member=False):
        """Initialize a Customer with name, contact info, and loyalty membership."""
        self._name = name
        self._contact_info = contact_info
        self._is_loyalty_member = is_loyalty_member
        self._shopping_cart = ShoppingCart()

    # Getter and Setter for name
    def get_name(self):
        """Get the customer's name."""
        return self._name

    def set_name(self, name):
        """Set the customer's name."""
        self._name = name

    # Getter and Setter for contact info
    def get_contact_info(self):
        """Get the customer's contact information."""
        return self._contact_info

    def set_contact_info(self, contact_info):
        """Set the customer's contact information."""
        self._contact_info = contact_info

    # Getter and Setter for loyalty membership
    def get_is_loyalty_member(self):
        """Check if the customer is a loyalty member."""
        return self._is_loyalty_member

    def set_is_loyalty_member(self, is_loyalty_member):
        """Set the customer's loyalty membership status."""
        self._is_loyalty_member = is_loyalty_member

    # Getter for shopping cart
    def get_cart(self):
        """Retrieve the customer's shopping cart."""
        return self._shopping_cart

    def __str__(self):
        """Return customer details as a string."""
        return f"Customer: {self._name}, Contact: {self._contact_info}, Loyalty Member: {self._is_loyalty_member}"


class EBook:
    """Class representing an eBook with title, author, publication date, genre, and price."""

    def __init__(self, title, author, publication_date, genre, price):
        """Initialize an eBook with title, author, publication date, genre, and price."""
        self._title = title
        self._author = author
        self._publication_date = publication_date
        self._genre = genre
        self._price = price

    # Getters and Setters for EBook attributes
    def get_title(self):
        """Get the eBook's title."""
        return self._title

    def set_title(self, title):
        """Set the eBook's title."""
        self._title = title

    def get_author(self):
        """Get the eBook's author."""
        return self._author

    def set_author(self, author):
        """Set the eBook's author."""
        self._author = author

    def get_publication_date(self):
        """Get the eBook's publication date."""
        return self._publication_date

    def set_publication_date(self, publication_date):
        """Set the eBook's publication date."""
        self._publication_date = publication_date

    def get_genre(self):
        """Get the eBook's genre."""
        return self._genre

    def set_genre(self, genre):
        """Set the eBook's genre."""
        self._genre = genre

    def get_price(self):
        """Get the eBook's price."""
        return self._price

    def set_price(self, price):
        """Set the eBook's price."""
        self._price = price

    def __str__(self):
        """Return eBook details as a string."""
        return f"{self._title} by {self._author} - {self._genre} - ${self._price}"


class EBookCatalog:
    """Class representing a catalog of eBooks."""

    def __init__(self, created_by="Admin"):
        """Initialize the eBook catalog."""
        self.ebooks = []
        self.date_created = datetime.now()
        self.date_modified = datetime.now()
        self.created_by = created_by

    # Getter and Setter for eBook catalog
    def get_ebooks(self):
        """Get the list of eBooks in the catalog."""
        return self.ebooks

    def set_ebooks(self, ebooks):
        """Set the list of eBooks in the catalog."""
        self.ebooks = ebooks
        self.date_modified = datetime.now()

    def add_ebook(self, ebook):
        """Add an eBook to the catalog."""
        self.ebooks.append(ebook)
        self.date_modified = datetime.now()

    def remove_ebook(self, title):
        """Remove an eBook from the catalog by its title."""
        self.ebooks = [ebook for ebook in self.ebooks if ebook.get_title() != title]
        self.date_modified = datetime.now()

    def list_ebooks(self):
        """Print the list of eBooks in the catalog."""
        for ebook in self.ebooks:
            print(ebook)

    def find_ebook(self, title):
        """Find an eBook in the catalog by its title."""
        for ebook in self.ebooks:
            if ebook.get_title() == title:
                return ebook
        return None

    def get_date_modified(self):
        return self.date_modified

    def get_date_created(self):
        return self.date_created

    def get_created_by(self):
        return self.created_by



class Invoice:
    """Class representing an invoice for an order."""

    VAT_RATE = 0.08

    def __init__(self, order):
        """Initialize an invoice with the associated order."""
        self.order_details = order
        self.invoice_date = datetime.now()
        self.total_with_vat = self.calculate_total_with_vat()
        self.status = "Pending Payment"

    # Getter and Setter for order details
    def get_order_details(self):
        """Get the details of the order."""
        return self.order_details

    def set_order_details(self, order):
        """Set the order details for the invoice."""
        self.order_details = order

    def calculate_total_with_vat(self):
        """Calculate the total price with VAT."""
        total = self.order_details.get_final_total()
        return total + (total * self.VAT_RATE)

    def get_status(self):
        return self.status

    def set_status(self):
        return self.status

    def __str__(self):
        """Return invoice details as a string."""
        return f"Invoice Date: {self.invoice_date}\n{self.order_details}\nTotal with VAT: ${self.total_with_vat:.2f}"


class Order:
    """Class representing a customer's order."""

    def __init__(self, customer, cart):
        """Initialize an order with the customer and their shopping cart."""
        self.order_date = datetime.now()
        self.order_items = cart.items.copy()
        self.total_price = cart.get_cart_total()
        self.customer = customer
        self.discount = self.calculate_discount()

    # Getters and Setters for Order attributes
    def get_order_date(self):
        """Get the order date."""
        return self.order_date

    def set_order_date(self, order_date):
        """Set the order date."""
        self.order_date = order_date

    def get_order_items(self):
        """Get the items in the order."""
        return self.order_items

    def set_order_items(self, order_items):
        """Set the items in the order."""
        self.order_items = order_items

    def get_total_price(self):
        """Get the total price of the order."""
        return self.total_price

    def set_total_price(self, total_price):
        """Set the total price of the order."""
        self.total_price = total_price

    def get_customer(self):
        """Get the customer for the order."""
        return self.customer

    def set_customer(self, customer):
        """Set the customer for the order."""
        self.customer = customer

    def get_discount(self):
        """Get the discount for the order."""
        return self.discount

    def set_discount(self, discount):
        """Set the discount for the order."""
        self.discount = discount

    def calculate_discount(self):
        """Calculate the discount for the order based on customer loyalty and bulk items."""
        discount = 0
        if self.customer.get_is_loyalty_member():
            discount += 0.10 * self.total_price  # 10% for loyalty members
        if len(self.order_items) >= 5:
            discount += 0.20 * self.total_price  # 20% for bulk orders
        return discount

    def get_final_total(self):
        """Calculate the final total price after applying the discount."""
        return self.total_price - self.discount

    def __str__(self):
        """Return order details as a string."""
        items = "\n".join([f"{ebook} x {qty}" for ebook, qty in self.order_items.items()])
        return f"Order Date: {self.order_date}\nItems:\n{items}\nDiscount: ${self.discount}\nTotal: ${self.get_final_total()}"


class ShoppingCart:
    """Class representing a shopping cart containing eBooks."""

    def __init__(self, created_by="Admin"):
        """Initialize the shopping cart with an empty list of items."""
        self.items = {}
        self.date_created = datetime.now()
        self.date_modified = datetime.now()
        self.created_by = created_by

    # Getter and Setter for shopping cart items
    def get_items(self):
        """Get the items in the shopping cart."""
        return self.items

    def set_items(self, items):
        """Set the items in the shopping cart."""
        self.items = items
        self.date_modified = datetime.now()

    def add_to_cart(self, ebook, quantity=1):
        """Add an eBook to the shopping cart."""
        if ebook in self.items:
            self.items[ebook] += quantity
        else:
            self.items[ebook] = quantity
        self.date_modified = datetime.now()

    def remove_from_cart(self, ebook):
        """Remove an eBook from the shopping cart."""
        if ebook in self.items:
            del self.items[ebook]
        self.date_modified = datetime.now()

    def get_cart_total(self):
        """Calculate the total price of items in the shopping cart."""
        return sum(ebook.get_price() * qty for ebook, qty in self.items.items())

    def list_cart_items(self):
        """Print the items in the shopping cart."""
        for ebook, qty in self.items.items():
            print(f"{ebook} x {qty}")

    def clear_cart(self):
        """Remove all items from the shopping cart."""
        self.items = {}
        self.date_modified = datetime.now()

    def get_date_modified(self):
        return self.date_modified

    def get_date_created(self):
        return self.date_created

    def get_created_by(self):
        return self.created_by
