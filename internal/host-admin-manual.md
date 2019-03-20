# Host Admin Manual

**Guide to managing Expenses for the Fiscal Hosts that Open Collective administrates.**

## Fiscal Hosts List <a id="docs-internal-guid-c63aa181-7fff-a12b-956a-0e66ccc70b1b"></a>

| Host | Paypal ID |
| :--- | :--- |
| [Open Source Collective](https://opencollective.com/opensourcecollective/collectives/expenses) 501\(c\)\(6\) | host+c6 |
| [Open Collective Host](https://opencollective.com/opencollective-host/collectives/expenses) c-corp | host |
| [Open Collective Foundation](https://opencollective.com/foundation/collectives/expenses) 501\(c\)\(3\) | host+c3 |
| [Open Collective Europe](https://opencollective.com/europe/collectives/expenses) | host+eu |
| [Open Collective Inc](https://opencollective.com/opencollectiveinc/collectives/expenses) \(internal\) | paypal |

## Expenses Payment Process

#### For expenses less than $2,000

1. Go to the dashboard of the host you want to process payments for.
2. Refill the Paypal pre-approval limit by clicking the button on the dashboard, logging into the correct Paypal for that host, and clicking “approve”. 
3. Return to the host dashboard.
4. Find an expense that has a green 'pay with paypal' button and is for less than $2,000. You can go one Collective at a time via the dropdown menu, or filter all by "approved".
5. Open the attached receipt or invoice and ensure it's [valid](../expenses/submitting-expenses.md#documentation-requirements).
6. Click the 'pay with paypal' button and pay the expense.

#### For expenses over $2,000

Paypal only allows pre-approval of $2,000 the pay via the API, so larger expenses have to be paid manually. 

1. Find an expense for over $2,000 that has a green button and open it in its own tab.
2. Check the attached receipt or invoice and ensure it's [valid](../expenses/submitting-expenses.md#documentation-requirements).
3. Open Paypal in another tab and go to 'send or receive money' and choose 'friends or family'.
4. Put in the user's email address and the amount.
5. Set the currency to USD for sending and receiving.
6. Past the URL of the expense as the note.
7. Complete the payment in Paypal.
8. Return to the expense page and click 'edit'.
9. Change the payment method to "other".
10. Save the expense and re-approve it.
11. Put the Paypal fee in the box if any.
12. Click 'record as paid'.

### Problems & Responses

1. Insufficient balance \(system will not allow payment\)
2. No valid receipt/invoice \(check attached file meets [requirements](../expenses/submitting-expenses.md#documentation-requirements)\)
3. Not enough funds to cover fees \(system will error and estimate fee amount\)
4. Not approved by core contributor \(no green ‘pay’ button\)   

If there is an issue with an expense, comment on it to notify the submitter.

**Note:** if you ask the user to do anything that requires them to edit the expense, you have to un-approve it first \(otherwise it's not editable by them\). To do this, edit the expense and make an insignificant change \(like adding a training space in the description\), then save it but don't click 'approve'.

#### Invoice or receipt missing or invalid

In order to reimburse the expense you submitted, it must have a valid invoice or receipt. If you need help, please see [our info about submitting expenses](../expenses/submitting-expenses.md). There's an invoice template available. Click 'Edit' on this expense to upload a new file.

#### Paypal address not provided

For the moment, we are only able to pay via Paypal. Please click 'edit' on your expense, select 'Paypal' from the dropdown menu, and input your Paypal email address. Thanks!

_**Note:** if you switch the payment method to Paypal yourself, it will pull in the user's email address. However, we can't assume that's the correct Paypal address as it might be different._

#### Fees not covered

Since your expense equals all the funds in the Collective, the system won’t put it through due to insufficient funds to cover the Paypal fees \($3\). Please click ‘edit’ and revise the amount to $3 less. Thank you!

**Note:** If you try to pay the expense, the system will tell you the estimated fee amount. You can also just reduce the amount of the expense yourself and just put it through, but inform the user with a comment so they aren't surprised by the reduced total.

### Special Cases

#### Do not touch

* ‘Idonethis’ expenses
* ‘Maintainer.io’ expenses

#### European Bank Transfer Payments

Collectives in the Europe host can request payment via bank transfer \(all other hosts can only pay with Paypal\). Compile a list of bank transfer expenses and give to Xavier to action.

### Tax Forms

We have on file [W9](https://www.dropbox.com/home/Open%20Source%20Collective%20501c6/IRS/W9) or [W8-BEN/E](https://www.dropbox.com/home/Open%20Source%20Collective%20501c6/IRS/W8-BEN) forms for users, which are required if we’re paying out $600 or more to a person in a year. The Tax Forms bot will let them know to send theirs through to us via a comment on the expense. Make sure we have one on file before paying an invoice for someone who has earned $600 or more. 

**Note:** this does not apply to expense reimbursements, only invoices.

## Adding Funds Manually

We have arrangements with several Collectives and Sponsors to accept funds outside the platform and add them manually.

| Host | Collective | Income | Notes |
| :--- | :--- | :--- | :--- |
| Foundation | SF Global Shapers | Eventbrite ticket sales |  |
| Foundation | Drupal Camp | T-shirts |  |
| OSC | Material-UI, BootstrapCDN | BuySellAds, CarbonAds | Go to [cashout](https://www.buysellads.com/sell/cashout), wait for Paypal payment, source = material-ui website |
| OSC | Webpack | Threadless |  |
| OSC | Material UI, BootstrapCDN, JSS | Consensys Codefund |  |
| OSC | Creative Tim | Avantgate | Report will come first, but wait for PayPal payment via 2Checkout |
| OSC | Nest | Valor Software | Transferwise |

### Process

1. Get email notification of payment \(different for each one\)
2. Confirm in Paypal or bank account
3. Go to host dashboard
4. Select Collective
5. Click add funds
6. Select funding source
7. Host fee 5%
8. 5% platform fee for OSC, 0% for Foundation

## Adding Host Fees

Open Collective charges a 5% host fee to Collectives. These funds need to be added manually each month to the host's Collective so they can use them to pay expenses.

Process:

1. Get monthly report
2. Find host fees
3. Go to host dashboard
4. Select host's Collective
5. Click Add Funds
6. 0% host fee
7. Source is that host



##   

