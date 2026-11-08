# AD361-LP06
## Step 1: Error Guessing

**Feature:** I choose creating a booking

Based on my experience with sites such as Airbnb, here are 3 things I think might go wrong:

- **Double booking:** The same rental can be booked twice for the same date, and both bookings go through.
- **Missing or invalid input accepted:** The form lets a user submit a booking without choosing a rental, with no guest count, or with a date in the past.
- **Booking not saved or not confirmed:** After clicking Confirm Booking, the user gets no confirmation, and the booking doesn't appear correctly (or disappears) on the Bookings page.

## Step 2: Exploratory Testing

**Charter:** Explore the Add Booking form with missing, duplicate, and unusual inputs to discover whether invalid bookings get saved or bookings fail to show correctly on the Bookings page.

| What I Tried                                                                       | What Happened                                                             | What I Decided to Try Next                            |
| ---------------------------------------------------------------------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------- |
| Opened the Rental dropdown on the Add Booking page                                 | The dropdown was empty, with no rentals to choose from                    | Submit the form without a date to see what's required |
| Left the date empty (guests defaulted to 1) and clicked Confirm Booking            | Blocked with "Please fill out this field" under Date                      | Pick a date and try 0 guests                          |
| Picked a date and entered 0 guests                                                 | Blocked with "Value must be greater than or equal to 1."                  | Try a very large guest count                          |
| Picked a date and entered 500 guests                                               | Booking was saved. Bookings page showed `Rental:` with **no rental name** | Try a past date                                       |
| Picked a past date (2025-03-05)                                                    | Booking was saved with no error                                           | Try booking the same thing twice                      |
| Submitted the same date (2026-12-11) and 7 guests twice                            | **Two identical bookings** appeared on the Bookings page                  | Check whether bookings stay after a refresh           |
| Refreshed the browser on the Bookings page                                         | **All bookings disappeared**                                              | Try clearing the guest field                          |
| Picked a date, deleted the number in Number of Guests, and clicked Confirm Booking | Booking was saved. Bookings page showed `Guests:` with no number          | Stop here                                             |

Future session idea: The Home page shows no rentals, and typing in the search bar does nothing. Test the Home page and search in a separate session.

## Step 3: Checklist-Based Testing

| Check                                         | Result         | Notes                                                          |
| --------------------------------------------- | -------------- | -------------------------------------------------------------- |
| Form cannot be submitted with an empty date   | Passed         | Shows "Please fill out this field"                             |
| Form cannot be submitted with 0 guests        | Passed         | Shows "Value must be greater than or equal to 1."              |
| Rental dropdown lists rentals to choose from  | Failed         | Dropdown is empty                                              |
| Saved booking includes a rental name          | Failed         | Every booking shows `Rental:` with no name                     |
| Past dates are rejected                       | Failed         | A booking for 2025-03-05 was saved                             |
| Guest count has a reasonable maximum          | Failed         | 500 guests was accepted                                        |
| The same booking can't be made twice          | Failed         | Two identical bookings for 2026-12-11 with 7 guests were saved |
| Booking shows a check-out date or total price | Unable to Test | The form has no check-out date or price fields                 |

## Step 4: Acceptance Testing

| Given, When, Then                                                                                                                                                                      | Result | Notes                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | --------------------------------------------------------------------- |
| Given I am on the Add Booking page, when I open the Rental dropdown, then I should see a list of rentals to choose from                                                                | Failed | The dropdown is empty                                                 |
| Given I am on the Add Booking page, when I submit a rental, a date, and 2 guests, then the booking should appear on the Bookings page with the same rental, date, and number of guests | Failed | No rental can be selected. The booking saves with a blank rental name |
| Given I have not picked a date, when I click Confirm Booking, then the booking should not be saved and I should be asked to choose a date                                              | Passed | Shows "Please fill out this field"                                    |
| Given I pick a date in the past, when I click Confirm Booking, then I should see an error and the booking should not be saved                                                          | Failed | The 2025-03-05 booking was saved                                      |
| Given I have already booked a date, when I submit the same booking again, then I should see an error and the second booking should not be saved                                        | Failed | Both bookings were saved with no warning                              |


