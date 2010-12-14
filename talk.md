!SLIDE

# Hello.

!SLIDE

# Pat Nakajima

!SLIDE

# I live in BROOKLYN.

!SLIDE

# patnakajima.com

!SLIDE

# github.com/nakajima

!SLIDE

# twitter.com/nakajima

!SLIDE

# bnter.com/nakajima

!SLIDE logo

<img src="https://groupme.s3.amazonaws.com/0-groupme-logo.png?AWSAccessKeyId=1YDBH46CVQ2V2X02WBR2&Expires=1361476255&Signature=71lBo8urhvFRr3y%2BWq3bHuPDTe4%3D">

# GroupMe

!SLIDE

## Free SMS chat rooms. Awesome.

!SLIDE hiring

# We are hiring.

!SLIDE

Ok. The talk STARTS NOW.

!SLIDE red

# Screw Cucumber

!SLIDE

# *Nah Just Playin...*

!SLIDE

But not really.

!SLIDE

# First thing is first.

!SLIDE green

# “Cucumber works for me!”

!SLIDE

# Then use it.

The plaque for the alternates is down in the ladies room. 

!SLIDE

# OK.

!SLIDE

# Cucumber: The Problems

By Pat Nakajima

!SLIDE

### Upgrades?

# More like SUCKgrades.

!SLIDE

# AM I RIGHT?

!SLIDE dark

### The real problem

# Step Definitions Are The Worst

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

# Wrong.

!SLIDE

# You WILL need custom steps

!SLIDE dark

Example

# Text message callbacks

!SLIDE

@@@ text
    Given I have a group with the number "484-123-1234"
    And I add "Pat" with the number "610-123-1234"
    And I add "Damon" with the number "302-123-1234"

!SLIDE

# Uh oh.

!SLIDE

## Instance variables in step definitions

!SLIDE

@@@ text
    Given @I have a @group with the number "484-123-1234"
    And @I add "Pat" with the number "610-123-1234"
    And @I add "Damon" with the number "302-123-1234"

!SLIDE

# Problem!

!SLIDE

# Which step sets which variables?

!SLIDE

# Too much state.

!SLIDE

### So what do we do?

# Parameterize our steps

!SLIDE small

@@@ text
    Given a group with the number "484-123-1234"
    And the group with the number "484-123-1234" adds "Pat" with the number "610-123-1234"
    And the group with the number "484-123-1234" adds "Brandon" with the number "302-123-1234"

!SLIDE

# Regular Expressions

!SLIDE

# Don't Care About Most of that

!SLIDE

# Need a beer to put out these flames.

!SLIDE

# So no instance variables...

!SLIDE

# And no parameterizing...

!SLIDE dark

### Too close for missiles.

# I’m switching to guns.

!SLIDE

# Inline your step definitions

!SLIDE

# Capybara with Steak

!SLIDE

# Sounds delicious.

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

# Still super readable

!SLIDE

@@@ text

    cat spec/acceptance/signup_spec.rb | grep '#'

!SLIDE

# You need to craft usable APIs

!SLIDE

# Testing is a means to an end.

!SLIDE

# You don’t want to be an expert in your test suite.

!SLIDE

# You want to be an expert in your domain.

!SLIDE

@@@ ruby

    group = create_group
    pat = create_user(:name => "Pat")
    group.add(pat)

!SLIDE

# Helpers Are Good

!SLIDE

@@@ ruby
    # When pat texts "#mute" to the group
    receive_text(
      :to => group.phone_number,
      :from => pat.phone_number,
      :text => "#mute"
    )

!SLIDE

# Your domain is better

!SLIDE

@@@ ruby

    class Group
      def muted_for?(user)
        membership_for(user).muted?
      end
    end

!SLIDE

@@@ ruby

    # Then he should be muted
    group.should be_muted_for(pat)

!SLIDE center

<img height="100%" src="http://www.saasta.fi/saasta/wp-content/uploads/2009/11/business.jpg">

!SLIDE

## “My business people read/write my .feature files”

!SLIDE

# They can still write the feature files.

!SLIDE

# You write the code.

!SLIDE

### It’s your job.

# You’re good at it.

!SLIDE

# Questions

Let Josh Knowles tell me how wrong I am for a while.

!SLIDE

# THANX! :)
