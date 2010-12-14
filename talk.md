!SLIDE

# Hello.

!SLIDE

# My name is Pat Nakajima

!SLIDE

# I live in Brooklyn.

### That’s right.

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

Ok. The talk starts NOW.

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

!SLIDE

# OK.

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

# You WILL need custom steps.

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

!SLIDE red

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

!SLIDE red

# Problem!

!SLIDE

# Regular Expressions

!SLIDE

# Don’t Care About Most of that

!SLIDE small

@@@ text
    Given a group with the number "484-123-1234"
    And the group with the number "484-123-1234" adds "Pat" with the number "610-123-1234"
    And the group with the number "484-123-1234" adds "Brandon" with the number "302-123-1234"

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
    group = create_group(:phone_number => "484-123-1234")

    # And the group adds "Pat" with the number "610-123-1234"
    pat = create_user(:name => "Pat", :phone_number => "610-123-1234")
    group.add pat

    # And the group adds "Damon" with the number "302-123-1234"
    damon = create_user(:name => "Damon", :phone_number => "302-123-1234")
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
    group.add(pat) # Good!

!SLIDE

@@@ ruby

    # Bad!
    group = create_user
    pat = create_user(:name => "Pat")
    add(group, pat) # No need for a test helper

!SLIDE

# Pick the right test helpers

!SLIDE

@@@ ruby
    # When pat texts "#mute" to the group
    receive_text(
      :to => group.phone_number,
      :from => pat.phone_number,
      :text => "#mute"
    )

!SLIDE

# Ctags for the friggin win.

!SLIDE

# Application Code > Test Helpers

!SLIDE

@@@ ruby

    # Then he should be muted
    group.should be_muted_for(pat)

!SLIDE

@@@ ruby

    class Group
      def muted_for?(user)
        membership_for(user).muted?
      end
    end

!SLIDE

# What About Web Steps?

!SLIDE

@@@ ruby

    # Given I have an user with developer features enabled
    user = create_user(:developer => true)
    
    # And a group
    group = create_group(:creator => user)

    # And I login
    login_as user

    # When I go to one of my groups
    visit "/groups/#{group.to_param}"

!SLIDE

@@@ ruby

    # This is tested on its own in sign_in_spec.rb
    def login_as(user)
      visit "/signin"
      fill_in "session[phone_number]", :with => user.email
      fill_in "session[password]", :with => "password"
      click_button "Sign In"
    end

!SLIDE

@@@ ruby
    # And I follow "Developer Stuff"
    click_link "Developer Area"

    # Then the group should have a bot
    group.reload.bot.should_not be_nil

    # Then I should see "Developer Area"
    page.should have_content("Developer Area")

    # And I should see my token
    page.should have_content(group.bot.token)

!SLIDE center

<img height="100%" src="http://www.saasta.fi/saasta/wp-content/uploads/2009/11/business.jpg">

!SLIDE

## “My business people read/write my .feature files”

!SLIDE

# They can still write the feature files.

!SLIDE

# You usually have to clean them up anyway.

!SLIDE

# So just write the code!

!SLIDE

### It’s your job.

# You’re good at it.

!SLIDE

# Questions?

Let Josh Knowles tell me how wrong I am for a while.

!SLIDE

# THANX! :)
