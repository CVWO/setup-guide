<!-- markdownlint-disable MD001 MD026 -->

# React on Rails Installation Guide

Guide for installing React on Rails 6 for the CVWO 2020/2021 Assignment.

If you face any issues during installation, please feel free to browse or post on [the forums](https://github.com/CVWO/installation-guide/issues) as other applicants might have the same problems.

## Introduction

#### What is _React_?

React is a JavaScript library created by Facebook. It is a User Interface (UI) library, which more simply put is a tool for building UI components (also known as frontend).

#### What is _Ruby on Rails_?

Ruby on Rails, also known as Rails, is a server-side (also known as backend) web application framework written in the Ruby language.

#### What is _React on Rails_?

Since the release of Rails 6 in August 2019, Webpacker (a JavaScript compiler) is built into Rails by default. This has made it easier for React and Rails to be integrated together, giving rise to a full-stack framework known unofficially as React on Rails. Given the widespread popularity of React, we have decided to include it in this assignment.

> **Note**: This is only one of the many ways to integrate React with Rails! Do check out **Section 4.3 - RESTful APIs** of the assignment PDF for another popular way to do so. This guide will only cover React on Rails.

## Installation and Setup

### 1. Install and Setup Ruby on Rails

Install and setup the latest version of Ruby on Rails with a database.

We recommend following this [Installation Guide by GoRails](https://gorails.com/setup/).

- If asked to choose the method of installing Ruby, we recommend using `rbenv` as it is used by CVWO projects, though it is not a requirement.

- For the choice of database, we recommend PostgreSQL as it is used by CVWO projects, but it is not a requirement.

At this point, you should be able to start building a simple Rails application (without React). You might want to checkout [this introductory tutorial to Ruby on Rails](https://guides.rubyonrails.org/getting_started.html) before moving on, especially if you have no prior Rails experience.

### 2. Integrating React with Rails

The following commands create a new Rails application called `my-app` in the current directory.

- If you are using PostgreSQL

```bash
rails new my-app --webpack=react -d postgresql
```

- If you are using SQLite 3 (Rails default)

```bash
rails new my-app --webpack=react
```

- If you are using MySQL

```bash
rails new my-app --webpack=react -d mysql
```

Move to the application directory

```bash
cd my-app
```

If you setup MySQL or PostgreSQL with a username/password, modify the `config/database.yml` file to contain the username/password that you specified

Create the database

```bash
rails db:create
```

Install the React Rails gem

```bash
bundle add react-rails
```

Generate a React installation

```bash
rails g react:install
```

At this point, if everything went well, you have successfully created a React on Rails application! Before moving on, you might want to familiarize yourself with React, especially if you have no prior React experience. Do check out [this introductory tutorial to React](https://reactjs.org/tutorial/tutorial.html).

### 3. A simple React on Rails application

#### Start the Rails application

To start the Rails application, use the following command:

```bash
rails server
```

Now go to your browser and go to `localhost:3000`. You should see a page that looks like this:

![Rails Startup Page](https://raw.githubusercontent.com/tiuweehan/React-Rails-Installation-Guide/master/assets/Rails%20Startup%20Page.png)

#### Generating a Basic Rails controller

Generate a controller using the following command:

```bash
rails generate controller Welcome index
```

This command does a few things:

- Creates a _Controller_ file at `app/controllers/welcome_controller.rb`
- Creates a _View_ file at `app/views/welcome/index.html.erb`
- Adds a route called `get welcome index` to the _Routes_ file at `config/routes.rb`

Now if you were to go to your browser and go to `localhost:3000/welcome/index`, you should see a page that looks like this:

![Welcome Index Page](https://raw.githubusercontent.com/tiuweehan/React-Rails-Installation-Guide/master/assets/Controller.png)

#### Generating React components

The following command creates a React component called `HelloWorld`:

```bash
rails g react:component HelloWorld greeting:string
```

This creates a _React Component_ file called "HelloWorld" at `app/javascript/components/HelloWorld.js`

Note: Your component is added to `app/javascript/components/` by default.

Now go to the `app/views/welcome/index.html.erb` you created in the previous step and add the following line to the bottom of the file:

```ruby
<%= react_component("HelloWorld", { greeting: "Hello from react-rails." }) %>
```

Now if you were to go to your browser and go to `localhost:3000/welcome/index`, you should see a page that looks like this:

![Welcome Index Page](https://raw.githubusercontent.com/tiuweehan/React-Rails-Installation-Guide/master/assets/React.png)

You have successfully integrated a React component into the file!

### 4. What now?

If you have made it this far, you are already halfway there!

Do note that the method above (embedding the React component directly into the view) is only one of many ways to integrate React with rails, though it is the simplest and most beginner friendly.

The more common and cleaner way to do it (and also how we do it in CVWO) is to use Rails as a REST API endpoint, with React reading the data from the endpoint. [This guide](https://dev.to/able/building-and-consuming-a-json-api-with-rails-and-react-42p6) provides a tutorial on a basic setup with such a design.

Now that you have a basic Rails setup, the rest is up to your imagination and a bit of wishful thinking. All the best for the rest of your assignment :)

### Credit

- This guide was first created by [Tiu Wee Han](https://github.com/tiuweehan), CVWO President for AY2019/2020
- [GoRails](https://gorails.com/setup)
- [Official documentation for the React Rails gem](https://github.com/reactjs/react-rails)
- [Getting started with Rails 6 and React by Spike Burton](https://medium.com/swlh/getting-started-with-rails-6-and-react-afac8255aecd)

© CVWO 2020/2021
