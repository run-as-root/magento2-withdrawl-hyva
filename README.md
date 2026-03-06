# Magento 2 Withdrawal – Hyvä Compatibility Module

A companion module for [Zwernemann_Withdrawal](https://github.com/Zwernemann/magento2-withdrawl) that replaces all frontend templates with Hyvä-compatible equivalents built on **Tailwind CSS** and **Alpine.js**.

---

## Base Module

The [magento2-withdrawl](https://github.com/Zwernemann/magento2-withdrawl) module implements the EU statutory right of withdrawal for Magento 2 stores. It covers the full workflow from the customer's initial request to the merchant's administrative handling.

### Features of the base module

**Customer side**
- Withdrawal button in the order history list and on the order detail page
- Dedicated withdrawal detail page showing order summary, ordered items, and the applicable deadline
- Guest customer support via a separate order search form
- Automatic confirmation email after a withdrawal has been submitted

**Merchant side**
- Admin grid listing all withdrawal requests with filtering and sorting
- Configurable withdrawal period (default: 14 days from shipment date)
- Automatic order comments on withdrawal submission
- Customisable transactional email templates
- REST API endpoint for programmatic access

**Technical**
- Supports Magento 2.4.6 – 2.4.8-p1
- Full translations for German and English (97 strings)
- CSRF protection on all forms
- ACL-based backend permissions

---

## This Module – Hyvä Compatibility

The default Magento frontend (Luma) uses RequireJS, Knockout.js, and LESS for its UI stack. [Hyvä Themes](https://hyva.io) replaces this stack with **Tailwind CSS** and **Alpine.js**, which means standard Luma templates are incompatible and render unstyled or broken in a Hyvä storefront.

This companion module solves that by providing a dedicated set of templates that follow Hyvä conventions – no Knockout, no RequireJS, no LESS.

### What is replaced / added

| Template | Description |
|---|---|
| `withdrawal/view.phtml` | Withdrawal detail page with order summary table, deadline display, and an Alpine.js confirmation modal before form submission |
| `withdrawal/success.phtml` | Success confirmation page with order reference and navigation links |
| `order/history/withdrawal_button.phtml` | Table cell for the order history list – shows the withdraw button, a "submitted" notice, or an "expired" notice depending on the order state |
| `order/history/column_header.phtml` | Column header cell for the withdrawal column in the order history table |
| `guest/search.phtml` | Guest order search form with Alpine.js form-state handling and HTML5 validation |
| `button.phtml` | Standalone button component linking to the withdrawal view |

### Key implementation details

- **Tailwind CSS** utility classes are used throughout for layout, typography, colour, and spacing – no custom LESS or CSS is added.
- **Alpine.js** handles interactive elements such as the confirmation modal (`x-data="{ showConfirm: false }"`) and submit-button disabling during form submission.
- CSRF form keys are included in every form, identical to the base module.
- Both logged-in customers and guests are fully supported.

---

## Requirements

| Dependency | Version |
|---|---|
| PHP | >= 7.4 |
| Magento | 2.4.6 – 2.4.8-p1 |
| zwernemann/module-withdrawal | >= 1.0.0 |
| hyva-themes/magento2-theme-module | * |

---

## Installation

```bash
composer require zwernemann/module-withdrawal-hyva
php bin/magento module:enable Zwernemann_WithdrawalHyva
php bin/magento setup:upgrade
php bin/magento cache:flush
```

---

## Usage

No additional configuration is required. Once enabled, the module's templates automatically take precedence over the base module's templates when a Hyvä theme is active. All configuration options from the base module remain available under **Stores → Configuration → Sales → Withdrawal**.

---

## Contributing

Contributions and bug reports are welcome. Please open an issue or pull request in this repository.

---

## License

[Open Software License 3.0 (OSL-3.0)](https://opensource.org/licenses/OSL-3.0)
