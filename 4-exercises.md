## Exercises

#### Challenge 1
Find and print out all academic positions that appear in leaders' prior experience (e.g. professor, dean, college instructor).

#### Challenge 2

After finding the academic positions, instead of replacing them with a common term (which means we loose more specific
information), try adding a new variable with a 1 if there is an academic position in the leader's list of prior
experiences, and 0 otherwise.

(HINT: In the csv file format, this means you'll need to add a comma followed by a 0 or 1 at the end of each line.
Try adding `,0` to the end of each line, then go through and change the `0` to a `1` if there's an
academic position in the line. Be sure to capture and keep the rest of the text on the line as-is. In Python or R,
you'll want to add a new column or new cell to each row.)

#### Challenge 3
Change the dates to a different format. Things you might want to do:
* You might only want two numbers for the year, to match with other data you have
(e.g. from 1/15/2000 to 1/15/00)
* You might want to add a zero in front of a single-digit month or day, to make the
date a standard length (e.g. from 1/15/2000 to 01/15/2000)
* When working with information for or from foreign countries, you might want to swap
the month and day numbers (e.g. from mm/dd/yy to dd/mm/yy).
