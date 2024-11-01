========
Colombia
========

.. |DIAN| replace:: :abbr:`DIAN (Dirección de Impuestos y Aduanas Nacionales)`

Odoo's Colombian localization package provides accounting, fiscal, and legal features for databases
in Colombia – such as chart of accounts, taxes, and electronic invoicing.The localization has the 
next `prerequisites <https://micrositios.dian.gov.co/sistema-de-facturacion-electronica/que-requieres
-para-factura-electronicamente/>`_ when using the `DIAN Own Software <hhttps://micrositios.dian.gov.
co/sistema-de-facturacion-electronica/como-puedes-facturar-electronicamente/>`_ solution with Odoo:

- Be registered in the `RUT <https://www.dian.gov.co/tramitesservicios/tramites-y-servicios/tributarios
/Paginas/RUT.aspx>`_ (Registro Único Tributario) with a valid NIT.
- Have a valid Digital Signature Certificate `approved by the ONAC <https://onac.org.co/directorio-de-
acreditados/>`_.
-`Register and get enabled <https://micrositios.dian.gov.co/sistema-de-facturacion-electronica/proceso
-de-registro-y-habilitacion-como-facturador-electronico/>`_ by completing the Certification Process 
required by the DIAN.

.. seealso::
   - For more information on how to complete the Certification process for the DIAN module, review the 
   following `Webinar <https://micrositios.dian.gov.co/sistema-de-facturacion-electronica/proceso
   -de-registro-y-habilitacion-como-facturador-electronico/>`_.
   - `Smart Tutorial - Colombian Localization
   <https://www.odoo.com/slides/smart-tutorial-localizacion-de-colombia-132>`_.

.. _colombia/configuration:

Configuration
=============

Modules installation
--------------------

:ref:`Install <general/install>` the following modules to get all the features of the Colombian
localization:

.. list-table::
   :header-rows: 1
   :widths: 25 25 50

   * - Name
     - Technical name
     - Description
   * - :guilabel:`Colombia - Accounting`
     - `l10n_co`
     - Default :ref:`fiscal localization package <fiscal_localizations/packages>`. This module adds
       the base accounting features for the Colombian localization: chart of accounts, taxes,
       withholdings, and identification document type.
   * - :guilabel:`Electronic invoicing for Colombia with DIAN`
     - `l10n_co_dian`
     - This module includes the features required for integration with the DIAN as an own software, Adds
       the ability to generate electronic invoices and support documents based on |DIAN| regulations.
   * - :guilabel:`Colombian - Accounting Reports`
     - `l10n_co_reports`
     - Includes accounting reports for sending certifications to suppliers for withholdings applied.
   * - :guilabel:`Electronic invoicing for Colombia with Carvajal`
     - `l10n_co_edi`
     - This module includes the features required for integration with Carvajal. Adds the ability to
       generate the electronic invoices and support documents, based on |DIAN| regulations.

.. note::
   When `Colombia` is selected for a company's :guilabel:`Fiscal Localization`, Odoo automatically
   installs certain modules.

Company configuration
---------------------

To configure your company information, go to the :menuselection:`Contacts` app, and search for your
company.

Alternatively, activate :ref:`developer mode <developer-mode>` and navigate to
:menuselection:`General Setting --> Company --> Update Info --> Contact`. Then, edit the contact
form and configure the following information:

- :guilabel:`Company Name`.
- :guilabel:`Address`: Including :guilabel:`City`, :guilabel:`Department` and :guilabel:`ZIP` code.
- :guilabel:`Identification Number`: Select the :guilabel:`Identification Type` (`NIT`, `Cédula de
  Ciudadanía`, `Registro Civil`, etc.). When the :guilabel:`Identification Type` is `NIT`, the
  :guilabel:`Identification Number` **must** have the *verification digit* at the end of the ID
  prefixed by a hyphen (`-`).

Next, configure the :guilabel:`Fiscal Information` in the :guilabel:`Sales & Purchase` tab:

- :guilabel:`Obligaciones y Responsabilidades`: Select the fiscal responsibility for the company
  (`O-13` Gran Contribuyente, `O-15` Autorretenedor, `O-23` Agente de retención IVA, `O-47` Regimen
  de tributación simple, `R-99-PN` No Aplica).
- :guilabel:`Gran Contribuyente`: If the company is *Gran Contribuyente* this option should be
  selected.
- :guilabel:`Fiscal Regimen`: Select the Tribute Name for the company (`IVA`, `INC`, `IVA e INC`,
  or `No Aplica`)
- :guilabel:`Commercial Name`: If the company uses a specific commercial name, and it needs to be
  displayed in the invoice.

Electronic Invoice Credentials configuration
--------------------------------------------

Once the modules are installed, the user credentials **must** be configured, in order to connect
with DIAN’s Web Service. To do so, navigate to :menuselection:`Accounting --> Configuration -->
Settings` and scroll to the :guilabel:`Colombian Electronic Invoicing` section. Then, fill in the
required configuration:

- Select :guilabel:`DIAN: Free Service` as the :guilabel:`Electronic Invoicing Provider`
- Configure the :guilabel:`Operation Mode(s)`: for the respective type(s) of document(s) to be 
generated from Odoo. For each type of document (Electronic Invoices or Support Documents) the next 
fields are required:
  #. :guilabel:`Software Mode`: Type of document to be generated with the operation mode.
  #. :guilabel:`Software ID`: ID generated by DIAN for the specific operation mode.
  #. :guilabel:`Software PIN`: PIN selected in the operation mode configuration in the DIAN portal
  #. :guilabel:`Testing ID`: Testing identification generated by DIAN and obtained from the testing 
  set of the operation mode
- Enter  your available **digital certificate** to sign your electronic documents:
  #. Both **Certificate** and **Certificate Key** must be in PEM format.
  
.. image:: colombia/dian-credentials-configuration.png
   :align: center 
   :alt: Colombian Electronic Invoicing credentials configured
   
.. note::
   In a multi-company database it is possible to have one certificate per company.

DIAN Environments Configuration  
-------------------------------

The DIAN Electronic Invoicing module offers three different DIAN environments to connect with:

- :guilabel:`Certification Environment`: This environment will be useful to pass the DIAN certification 
  process and obtain the enabled status to invoice from Odoo. To activate it, go to  
  :menuselection:`Accounting --> Configuration --> Settings` and enable both the *Test Environment* and  
  the *Activate the certification process* checkboxes.

- :guilabel:`Testing Environment`: This environment allows reproducing Electronic Invoicing flows and 
  validations in the DIAN testing portal. To activate it, go to :menuselection:`Accounting --> 
  Configuration --> Settings` and check the *Test Environment* checkbox only.

- :guilabel:`Production Environment`: Activate production databases to generate valid electronic documents.  
  To activate it, go to :menuselection:`Accounting --> Configuration --> Settings` and disable both  
  the *Test Environment* and the *Activate the certification process* checkboxes.

.. seealso::  
   For Electronic Invoicing Configurations using the Carvajal solution, review the following  
   `video <https://www.youtube.com/watch?v=bzweMwTEbfY&list=PL1-aSABtP6ABxZshems3snMjx7bj_7ZsZ&index=3>`_.

Report data configuration
-------------------------

Report data can be defined for the fiscal section and bank information of the PDF as part of the
configurable information sent in the XML.

Navigate to :menuselection:`Accounting --> Configuration --> Settings`, and scroll to the
:guilabel:`Colombian Electronic Invoicing` section, in order to find the :guilabel:`Report
Configuration` fields. Here the header information for each report type can be configured.

- :guilabel:`Gran Contribuyente`
- :guilabel:`Tipo de Régimen`
- :guilabel:`Retenedores de IVA`
- :guilabel:`Autorretenedores`
- :guilabel:`Resolución Aplicable`
- :guilabel:`Actividad Económica`
- :guilabel:`Bank Information`

.. _colombia/master-data:

Master data configuration
-------------------------

Partner
~~~~~~~

Partner contacts can be created in the *Contacts* app. To do so, navigate to
:menuselection:`Contacts`, and click the :guilabel:`Create` button.

Then, name the contact, and using the radio buttons, select the contact type, either
:guilabel:`Individual` or :guilabel:`Company`.

Complete the full :guilabel:`Address`, including the :guilabel:`City`, :guilabel:`State`, and
:guilabel:`ZIP` code. Then, complete the identification and fiscal information.

Identification information
**************************

Identification types, defined by the |DIAN|, are available on the partner form, as part of the
Colombian localization. Colombian partners **must** have their :guilabel:`Identification Number`
(VAT) and :guilabel:`Document Type` set.

.. tip::
   When the :guilabel:`Document Type` is `NIT`, the :guilabel:`Identification Number` needs to be
   configured in Odoo, including the *verification digit at the end of the ID, prefixed by a hyphen
   (`-`)*.

Fiscal information
******************

The partner's responsibility codes (section 53 in the :abbr:`RUT (Registro único tributario)`
document) are included as part of the electronic invoicing module, as it is required by the |DIAN|.

The required fields can be found under :menuselection:`Partner --> Sales & Purchase Tab --> Fiscal
Information section`:

- :guilabel:`Obligaciones y Responsabilidades`: Select the fiscal responsibility for the company
  (`O-13` Gran Contribuyente, `O-15` Autorretenedor, `O-23` Agente de retención IVA, `O-47` Regimen
  de tributación simple, or `R-99-PN` No Aplica).
- :guilabel:`Gran Contribuyente`: If the company is *Gran Contribuyente* this option should be
  selected.
- :guilabel:`Fiscal Regimen`: Select the tribute name for the company (`IVA`, `INC`, `IVA e INC`, or
  `No Aplica`)
- :guilabel:`Commercial Name`: If the company uses a specific commercial name, and it needs to be
  displayed in the invoice.

Products
~~~~~~~~

To manage products, navigate to :menuselection:`Accounting --> Customers --> Products`, then click
on a product.

When adding general information on the product form, it is required that either the
:guilabel:`UNSPSC Category` (:guilabel:`Accounting` tab), or :guilabel:`Internal Reference`
(:guilabel:`General Information` tab) field is configured. Be sure to :guilabel:`Save` the product
once configured.

Taxes
~~~~~

To create or modify taxes, go to :menuselection:`Accounting --> Configuration --> Taxes`, and select
the related tax.

If sales transactions include products with taxes, the :guilabel:`Value Type` field in the
:guilabel:`Advanced Options` tab needs to be configured per tax. Retention tax types
(:guilabel:`ICA`, :guilabel:`IVA`, :guilabel:`Fuente`) are also included. This configuration is used
to display taxes correctly in the invoice PDF.

.. image:: colombia/DIAN-taxes-configuration.png
   :align: center 
   :alt: Specific tax configurations per DIAN regulations

.. _co-journals:

Sales journals
~~~~~~~~~~~~~~

Once the |DIAN| has assigned the official sequence and prefix for the electronic invoice resolution,
the sales journals related to the invoice documents **must** be updated in Odoo. To do so, navigate
to :menuselection:`Accounting --> Configuration --> Journals`, and select an existing sales journal,
or create a new one with the :guilabel:`Create` button.

On the sales journal form, input the :guilabel:`Journal Name`, :guilabel:`Type`, and set a unique
:guilabel:`Short Code` in the :guilabel:`Journals Entries` tab. Then, configure the following data
in the :guilabel:`Advanced Settings` tab:

-:guilabel:`Electronic invoicing`: Enable UBL 2.1 (Colombia).
-:guilabel:`Invoicing Resolution`: Resolution number issued by DIAN to the company via their test set.
-:guilabel:`Resolution Date`: Initial effective date of the resolution.
-:guilabel:`Resolution End Date`: End date of the resolution’s validity.
-:guilabel:`Range of Numbering (minimum)`: First authorized invoice number.
-:guilabel:`Range of Numbering (maximum)`: Last authorized invoice number.
-:guilabel:`Technical Key`: Control key received from the DIAN portal test set or from their web service 
in case of the production environment.

When the database is configured for the **production environment**, instead of configuring these fields 
manually, use the **Reload DIAN configuration** button to obtain the DIAN Resolution information from the required 
DIAN web service.

.. image:: colombia/Reload-DIAN-configuration-button.png
   :align: center 
   :alt: Reload DIAN configuration button in Sale Journals

.. important::
   The short code and resolution of the journal **must** match the ones received in the DIAN portal test set 
   or from the **MUISCA** portal.

Invoice sequence
****************

The invoice sequence and prefix **must** be correctly configured when the first document is created.

.. note::
   Odoo automatically assigns a prefix and sequence to the following invoices.

Purchase journals
*****************

Once the |DIAN| has assigned the official sequence and prefix for the *support document* related to
vendor bills, the purchase journals related to their supporting documents need to be updated in
Odoo. The process is similar to the configuration of the :ref:`sales journals <co-journals>`.

.. seealso::  
   For more information on Support Document Journals using the Carvajal solution review the following
   `video <https://www.youtube.com/watch?v=UmYsFcD7xzE&list=PL1-aSABtP6ABxZshems3snMjx7bj_7ZsZ&index=8>`_.

Chart of accounts
*****************

The :doc:`chart of accounts </applications/finance/accounting/get_started/chart_of_accounts>` is
installed by default as part of the localization module, the accounts are mapped automatically in
taxes, default account payable, and default account receivable. The chart of accounts for Colombia
is based on the PUC (Plan Unico de Cuentas).

.. _colombia/workflows:

Main workflows
==============

Electronic invoices
-------------------

The following is a breakdown of the main workflow for electronic invoices with the Colombian localization:

1. Sender creates an invoice.
2. Odoo generates the legal XML file.
3. Odoo generates the CUFE (Invoice Electronic Code) with the electronic signature.
4. Odoo sends a notification to DIAN.
5. DIAN validates the invoice.
6. DIAN accepts or rejects the invoice.
7. Odoo generates the PDF invoice with a QR code.
8. Odoo compresses the AttachedDocument (containing the sent XML file and the DIAN validation response) 
and the fiscal valid PDF into a :file:`.zip` file
9. User sends the invoice (:file:`.zip` file) via Odoo to the acquirer.

.. _colombia/invoice-creation:

Invoice creation
~~~~~~~~~~~~~~~~

.. note::
   The functional workflow taking place before an invoice validation does **not** alter the main
   changes introduced with the electronic invoice.

Electronic invoices are generated and sent to both the |DIAN| and customer. These documents can be created 
from your sales order or manually generated. To create a new invoice, go to 
:menuselection:`Accounting --> Costumers --> Invoices`, and select **Create**. On the invoice form configure 
the following fields:

-:guilabel:`Customer`: Customer’s information.
-:guilabel:`Journal`: Journal used for electronic invoices.
-:guilabel:`Electronic Invoice Type`: Select the type of document. By default, Factura de Venta is selected.
-:guilabel:`Invoice Lines`: Specify the products with the correct taxes.

.. important::
   When creating the first invoice related to an Electronic Invoicing Journal, it is required to manually change the 
   **sequence** of the invoice to the DIAN format corresponding to the `Prefix + Sequence`.
   **Example**: From `SETP1/2024/00001` to `SETP1`

When done, click :guilabel:`Confirm`.

.. _colombia/invoice-validation:

Sending Electronic Invoices
~~~~~~~~~~~~~~~~~~~~~~~~~~~

After the invoice confirmation, click on the **Print & Send** button. In the appearing wizard, make sure to enable the 
**DIAN** and **Email** checkboxes to send an XML to the DIAN web service and the validated invoice to your client 
fiscal email. After that, click on the Print & Send button:

- The XML document is created
- CUFE is generated
- The XML is processed synchronously by the DIAN. 
- If accepted, the file is displayed in the chatter and also the email to the client with the corresponding 
:file:`.zip` file.

.. image:: colombia/zip-xml-chatter-colombia.png
   :align: center 
   :alt: EDI documents available in the chatter
   
The **DIAN tab** will now displayed and the next information will be available in the record shown:

-:guilabel:`Signed Date`: Timestamp recorded of the XML creation.
-:guilabel:`Status`: The status result obtained in the DIAN response. If the invoice was rejected, the 
error messages can be seen here.
-:guilabel:`Testing Environment`: This checkbox will let us know if the document sent was delivered to 
the DIAN testing environment.
-:guilabel:`Certification Process`: This checkbox will let us know if the document was sent as part of 
the certification process with the DIAN.
-:guilabel:`Download button`: With this button, it is possible to download the sent XML file, even if 
the DIAN result was “Rejected”.
-:guilabel:`Fetch Attached Document button`: With this button, it is possible to download the 
generated AttachedDocument file, even if the DIAN.

.. image:: colombia/dian-tab-electronic-document.png
   :align: center 
   :alt: EDI document record available in DIAN tab

Credit notes
------------

The process for credit notes is the same as for invoices. To create a credit note with reference to
an invoice, go to :menuselection:`Accounting --> Customers --> Invoices`. On the invoice, click
:guilabel:`Add Credit Note`, and complete the following information:

- :guilabel:`Credit Method`: Select the type of credit method.

  - :guilabel:`Partial Refund`: Use this option when it is a partial amount.
  - :guilabel:`Full Refund`: Use this option if the credit note is for the full amount.
  - :guilabel:`Full refund and new draft invoice`: Use this option if the credit note is
    auto-validated and reconciled with the invoice. The original invoice is duplicated as a new
    draft.

- :guilabel:`Reason`: Enter the reason for the credit note.
- :guilabel:`Reversal Date`: Select if you want a specific date for the credit note or if it is the
  journal entry date.
- :guilabel:`Use Specific Journal`: Select the journal for your credit note or leave it empty if
  you want to use the same journal as the original invoice.
- :guilabel:`Refund Date`: If you chose a specific date, select the date for the refund.

Once reviewed, click the :guilabel:`Reverse` button.

Debit notes
-----------

The process for debit notes is similar to credit notes. To create a debit note with reference to an
invoice, go to :menuselection:`Accounting --> Customers --> Invoices`. On the invoice, click the
:guilabel:`Add Debit Note` button, and enter the following information:

- :guilabel:`Reason`: Type the reason for the debit note.
- :guilabel:`Debit note date`: Select the specific options.
- :guilabel:`Copy lines`: Select this option if you need to register a debit note with the same
  lines of invoice.
- :guilabel:`Use Specific Journal`: Select the printer point for your debit note, or leave it empty
  if you want to use the same journal as the original invoice.

When done, click :guilabel:`Create Debit Note`.

Support document for vendor bills
---------------------------------

With master data, credentials, and the purchase journal configured for support documents related to
vendor bills, you can start using *support documents*.

Support documents for vendor bills can be created from your purchase order or manually. Go to
:menuselection:`Accounting --> Vendors --> Bills` and fill in the following data:

- :guilabel:`Vendor`: Enter the vendor's information.
- :guilabel:`Bill Date`: Select the date of the bill.
- :guilabel:`Journal`: Select the journal for support documents related to the vendor bills.
- :guilabel:`Invoiced Lines`: Specify the products with the correct taxes.

Once reviewed, click the :guilabel:`Confirm` button. Upon confirmation, an XML file is created and
automatically sent to Carvajal.

.. _colombia/common-errors:

Common errors
-------------

During the XML validation, the most common errors are related to missing master data (*Contact Tax
ID*, *Address*, *Products*, *Taxes*). In such cases, error messages are shown in the chatter after
updating the electronic invoice status.

.. image:: colombia/validation-error-example-DIAN.png
   :align: center 
   :alt: Validation error example before sending electronic documents to the DIAN

If the invoice was sent and set as **Rejected** by the DIAN, the error messages are visible clicking in 
the **“i”** symbol next to the **Status** field in the **DIAN tab**. Using the reported error codes, it will be 
possible to review solutions to apply before re-sending.

.. image:: colombia/rejected-invoice-error-message.png
   :align: center 
   :alt: Example of error messages on rejected invoices

After the master data or other issues are corrected, it’s possible to reprocess the XML following again the 
:doc:`Sending Electronic Invoices <documentation/content/applications/finance/fiscal_localizations/colombia
/main_workflow/electronic_invoices/sending_electronic_invoices>` flow.

.. _colombia/reports:

Financial reports
=================

Certificado de Retención en ICA
-------------------------------

This report is a certification to vendors for withholdings made for the Colombian Industry and
Commerce (ICA) tax. The report can be found under :menuselection:`Accounting --> Reporting -->
Colombian Statements --> Certificado de Retención en ICA`.

.. image:: colombia/ica-report.png
   :align: center
   :alt: Certificado de Retención en ICA report in Odoo Accounting.

Certificado de Retención en IVA
-------------------------------

This report issues a certificate on the amount withheld from vendors for VAT withholding. The report
can be found under :menuselection:`Accounting --> Reporting --> Colombian Statements --> Certificado
de Retención en IVA`.

.. image:: colombia/iva-report.png
   :align: center
   :alt: Certificado de Retención en IVA report in Odoo Accounting.

Certificado de Retención en la Fuente
-------------------------------------

This certificate is issued to partners for the withholding tax that they have made. The report can
be found under :menuselection:`Accounting --> Reporting --> Colombian Statements --> Certificado de
Retención en Fuente`.

.. image:: colombia/fuente-report.png
   :align: center
   :alt: Certificado de Retención en Fuente report in Odoo Accounting.
