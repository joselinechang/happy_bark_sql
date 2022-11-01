# happy_bark_sql
--Happy bark scrip coderhouse proyecto final

USE happy_bark;

-- Tabla No. 1 Ventas

CREATE TABLE sales (
id_sale INT NOT NULL AUTO_INCREMENT,
shipping_id INT NULL,
id_client INT NOT NULL,
discount_percentage VARCHAR(30) NULL,
sale_date DATE NOT NULL,
bill_number INT NOT NULL,
total DECIMAL NOT NULL,
PRIMARY KEY (id_sale),
FOREIGN KEY (shipping_id) REFERENCES shipping(shipping_id),
FOREIGN KEY (id_client) REFERENCES client(id_client),
FOREIGN KEY (discount_percentage) REFERENCES discount(discount_percentage)
);

-- NO.2 Tabla de envios, agregar dos datos 1. precio mayoreo 2.precio local 3. precio de temporada descuento.

CREATE TABLE shipping (
    shipping_id INT NOT NULL AUTO_INCREMENT,
    shipping_cost INT NULL,
    PRIMARY KEY (shipping_id)
);

-- NO. 3Tabla productos, agregar los 8 productos con gramos incluidos en el nombre--

 CREATE TABLE product (
    product_name VARCHAR(20) NOT NULL,
    product_type TEXT(20) NOT NULL,
    description VARCHAR(30) NULL,
    PRIMARY KEY (product_name (20))
);

-- NO. 4 DRY STOCK, productos en inventario

CREATE TABLE dry_stock (
    id_stock INT NOT NULL AUTO_INCREMENT,
    product_name VARCHAR(20) NOT NULL,
    amount_in_stock INT NOT NULL,
    amount_taken INT NOT NULL,
    date_of_removal DATE NOT NULL,
    expiration_date DATE NOT NULL,
    PRIMARY KEY (id_stock),
    FOREIGN KEY (product_name)
        REFERENCES product (product_name)
);

-- Tabla 5. Discounts dependiendo la temporada

CREATE TABLE discount (
discount_percentage VARCHAR(30) NOT NULL,
discount_name TEXT(10) NOT NULL,
discount_date DATE NOT NULL,
description TEXT(10) NOT NULL,
PRIMARY KEY (discount_percentage(30))
);

-- tabla numero 7 ya sea mayoreo o menudeo
CREATE TABLE clients_type (
    client_type TEXT(10) NOT NULL,
    PRIMARY KEY (client_type (10))
);

-- Tabla No. 6 CLIENT- veterinarias y gente regular

CREATE TABLE client (
id_client INT NOT NULL AUTO_INCREMENT, 
client_type TEXT(10) NOT NULL,
client_name TEXT(50) NOT NULL,
client_address VARCHAR(30) NULL,
client_phone_number INT NULL,
email VARCHAR(20) NULL,
PRIMARY KEY (id_client),
FOREIGN KEY (client_type (10)) REFERENCES clients_type (client_type)
);

-- Tabla numero 9  Tipo de pago proveedor, servicios u otros

CREATE TABLE payments_type (
    payment_type TEXT(10) NOT NULL,
    description VARCHAR(30) NULL,
    PRIMARY KEY (payment_type (10))
);

-- Tabla numero 8 Pagos

CREATE TABLE payments (
id_payments INT NOT NULL AUTO_INCREMENT,
payment_type TEXT(10) NOT NULL,
amount DECIMAL(15,2) NOT NULL,
payment_date DATE NOT NULL,
payment_bill_number INT NULL,
PRIMARY KEY (id_payments),
FOREIGN KEY (payment_type(10)) REFERENCES payments_type (payment_type)
);

-- Tabla numero 11 meat provider

CREATE TABLE meat_provider (
provider_name VARCHAR(30) NOT NULL,
provider_phone_number INT NOT NULL,
protein_name TEXT (10) NOT NULL,
PRIMARY KEY (protein_name(10))
);

-- tabla numero 10 raw food provider

CREATE TABLE raw_food_provider (
id_raw_stock INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
protein_name TEXT(10) NOT NULL,
kilograms INT NOT NULL,
raw_date DATE NOT NULL,
FOREIGN KEY (protein_name(10)) REFERENCES meat_provider (protein_name)
);
