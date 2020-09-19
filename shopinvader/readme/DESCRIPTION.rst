This is shopinvader the odoo module for the new generation of e-commerce.

ShopInvader is an ecommerce software to create and manage easily your online store with Odoo.

This is the Odoo side of the `Shopinvader E-commerce Solution`_.

.. _Shopinvader E-commerce Solution: https://shopinvader.com

Technical
~~~~~~~~~

Data is exposed by services. Most of services for odoo models is already defined in this repository.
Each public method in service becomes public on service reachable for endpoint.
To declare a method you also need to declare a validator for that method:

Example:

.. code-block:: python

  from odoo.addons.component.core import Component

    class CartService(Component):
        _inherit = "shopinvader.abstract.sale.service"
        _name = "shopinvader.cart.service"
        _usage = "cart"

        def add_item(self, **params):
            return self._to_json(cart)

        def _validator_add_item(self):
            return {
                "lines": {
                    "type": "list",
                    "required": True,
                    "schema": {
                        "type": "dict",
                        "schema": self._validator_add_item(),
                    },
                }
            }

Data to expose need to be described in schema. Validation process is done with python library Cerberus.
https://docs.python-cerberus.org/en/stable/
The most common used attributes in schemas:

- "type" - data type values : string, integer, float, binary, dict, list
- "required" - boolean
- "empty" - boolean
- "nullable": - boolean

Testing
~~~~~~~

To check and test services you can use swagger extension which automatically parses services and it's public methods



Configuration
~~~~~~~~~~~~~
