+++
title = "appreciating django templates"
date = 2008-04-06
description = "ode-to-a-template-architecture"
authors = []

[taxonomies]
tags=[ "django" ]
+++

I'm loving [Django](http://www.djangoproject.com/) [templates](http://www.djangoproject.com/documentation/templates/).

In setting up a site for my bookgroup, I used a model for 'Meeting' that has a 'meeting_date' defined as a 'DateTimeField'. For those who haven't yet tasted the Django kool-aid, that's a field that requires both a valid date and a valid time. Made sense to me, since one of the main reasons for the site is to be able to list the location and date & time of upcoming meetings. However, when entering a few old meetings, the spreadsheet I was working from only listed the month and year (November 1997! -- we've been around for a while!).

There were a couple of ways I could have handled this. What I chose to do was to add two boolean fields: 'fake_date' (meaning 'day') and 'fake_time'. It might have been cleaner to allow we admins to have a year, a month, a date, and a time field -- but I knew going forward the single DateTimeField would work for us and I wanted to build more for the future than the past. So, when entering an old meeting with just a month and year, any date in that month is entered and any time of day, and both fake_date and fake_time are checked.

The complete DateTime object is passed to the template, and then some logic goes to work:

    {% if meeting.fake_date %}
        <h2>{{ meeting.date_time|date:\"F, Y\"|lower }}</h2>
    {% else %}
        {% if meeting.fake_time %}
            <h2>{{ meeting.date_time|date:\"l, F jS, Y\"|lower }}</h2>
        {% endif %}
    {% endif %}
    
    {% if not meeting.fake_date and not meeting.fake_time %}
        <h2>{{ meeting.date_time|date:\"l, F jS, Y g:iA\"|lower }}</h2>
    {% endif %}

I could have more efficiently handled the 'happy-path' real-date case via nesting, but I find this a bit more readable.

If the first test matches, the DateTime object info will only show, as an example, 'march 1998'; if the second test matches, the same DateTime object will only show 'march 6, 1998', but not the time.

This is nice. My introduction to templates was in Java, via JSPs, using expression-language to pass in values from beans. Since pure java code can be embedded in JSPs, I had trained myself to rigidly keep logic out of templates, and in the above situation would have written that logic within a Java class. When I began working more with php, I looked around for a template system. I had heard good things about 'smarty', but it seemed too heavyweight. That, combined with my fierce aversion to template logic, scared me off. I then attended a *wonderful* presentation on HTML_Template_ITX, was sold whole-hog, and still use that for my php end-user web work. 

What I initially loved about Django's templates is that I didn't have to use any of the logical conditions I show above; it can be used very well very simply. As I've grown more comfortable with Django and python, my philosophical aversion to template-logic has gradually diminished -- as long as it's *presentation* logic. The situation above is a perfect example: It's very reasonable for the business-logic end of things to pass to the presentation-layer a date. How that date is then formatted (upper or lowercase, whether or not the day or other elements of the date are shown, etc.) is a very reasonable thing for the template to handle. And that the template can also handle the presentation based on certain conditions of the Meeting instance is very, *very*, nice.
