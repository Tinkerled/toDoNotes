
todo:
Make calendar keyboard accessible
Follow example of Lightning input date

Fix disabled Sunday

date range input:

Scenario click
    click date input => open date dialog
    click date OR click outside => close dialog

Scenario tabs
    tab into input => focus input.
    tab calendar icon => focus calendar icon
    enter on calendar icon => open calendar on date
    click date => close dialog + return focus to calendar icon


Current focus management:
    click input => open calendar
    click date => blur input -> close calendar

    ::: blur input should not hide calendar if focus is in calendar
