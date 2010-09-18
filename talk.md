!SLIDE red

# Screw Cucumber

!SLIDE

# *Nah Just Playin...*

!SLIDE

But not really.

!SLIDE

# @nakajima

!SLIDE

# github.com/nakajima

!SLIDE

# GroupMe

!SLIDE

# The Problem with Cucumber

!SLIDE

# Step Definitions

!SLIDE

@@@ ruby
    When /^(?:|I )go to (.+)$/ do |page_name|
      visit path_to(page_name)
    end

    When /^(?:|I )press "([^\"]*)"$/ do |button|
      click_button(button)
    end

    When /^(?:|I )follow "([^\"]*)"$/ do |link|
      click_link(link)
    end

    When /^(?:|I )fill in "([^\"]*)" with "([^\"]*)"$/ do |field, value|
      fill_in(field, :with => value)
    end

!SLIDE

# Not so bad, RIGHT?

!SLIDE

# Do you know about life?

Things fall apart.

!SLIDE

Example

# Text message callbacks

!SLIDE

@@@ text
    Given a group with the number "484-123-1234"
    And the group adds "Pat" with the number "610-123-1234"
    And the group adds "Damon" with the number "302-123-1234"

!SLIDE

# Uh oh.

!SLIDE

@@@ text
    Given a @group with the number "484-123-1234"
    And the @group adds "Pat" with the number "610-123-1234"
    And the @group adds "Damon" with the number "302-123-1234"

!SLIDE

## Instance variables in step definitions = PAIN

!SLIDE

<small><pre>Given a group with the number "484-123-1234"
And the group with the number "484-123-1234" adds "Pat" with the number "610-123-1234"
And the group with the number "484-123-1234" adds "Pat" with the number "610-123-1234"</pre>
</small>

!SLIDE

## Parameterizing steps = PAIN

!SLIDE

# So no instance variables...

!SLIDE

# And no parameterizing...

!SLIDE

# YOU’RE TEARING ME APART CUCUMBER!

!SLIDE

# Solution?

!SLIDE

# Inline your step definitions

!SLIDE

@@@ ruby
    # Given a group with the number "484-123-1234"
    group = create_group

    # And the group adds "Pat" with the number "610-123-1234"
    pat = create_user(:name => "Pat")
    group.add pat

    # And the group adds "Damon" with the number "302-123-1234"
    damon = create_user(:name => "Damon")
    group.add damon

!SLIDE

# But what about web steps?

!SLIDE

# Use Steak

!SLIDE

# http://github.com/cavalle/steak

!SLIDE

# It's just Capybara

!SLIDE center

<img height="100%" src="http://www.saasta.fi/saasta/wp-content/uploads/2009/11/business.jpg">

!SLIDE

## “My business people read/write my .feature files”

!SLIDE

# They can still write the feature files.

!SLIDE

# You write the code.

!SLIDE

# It’s your job.

And you’re good at it.

!SLIDE

# THANX! :)