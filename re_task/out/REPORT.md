# Per-tier SaaS dashboard + billing best practice

Question: From open-source SaaS starters and docs (Supabase, Stripe/Lemon Squeezy billing portals, usage metering, plan gating, per-plan feature flags): how to build tier-specific dashboards (Starter/Pro/Team/Scale), usage meters, upgrade prompts, billing page, invoices, seat management, template counts per plan.

Sources read: 2 (public only). Model: @cf/meta/llama-3.1-8b-instruct-fast via Cloudflare Workers AI free tier.

## Playbook

**Tier-specific dashboards, usage meters, upgrade prompts, billing page, invoices, seat management, and template counts per plan: A Practical Playbook**

**Tools and Licenses:**

* Supabase (PostgreSQL database with Row Level Security and API): Free (open-source) and paid plans
* Lemon Squeezy (customer portal and subscription management): Free trial, then paid plans
* Stripe (payment gateway): Free trial, then paid plans

**Step-by-Step Guide:**

1. **Set up Supabase:**
	* Create a new Supabase instance and set up a PostgreSQL database.
	* Enable Row Level Security (RLS) and create a new role for each tier (e.g., `starter`, `pro`, `team`, `scale`).
2. **Create tier-specific tables:**
	* Create separate tables for each tier to store tier-specific data (e.g., `starter`, `pro`, `team`, `scale`).
	* Use RLS to restrict access to tier-specific data based on the user's role.
3. **Implement usage meters:**
	* Create a `usage` table to store usage data for each user.
	* Use a trigger function to update the usage data whenever a user performs an action (e.g., creates a new template).
	* Create a policy to restrict access to usage data based on the user's role.
4. **Implement upgrade prompts:**
	* Create a `plans` table to store information about each plan (e.g., `starter`, `pro`, `team`, `scale`).
	* Use a trigger function to update the user's plan whenever they upgrade.
	* Create a policy to restrict access to plan information based on the user's role.
5. **Implement billing page:**
	* Create a `invoices` table to store invoice data for each user.
	* Use a trigger function to update the invoice data whenever a user is charged.
	* Create a policy to restrict access to invoice data based on the user's role.
6. **Implement seat management:**
	* Create a `seats` table to store information about each user's seats (e.g., number of users, number of templates).
	* Use a trigger function to update the seat data whenever a user is added or removed.
	* Create a policy to restrict access to seat data based on the user's role.
7. **Implement template counts per plan:**
	* Create a `templates` table to store information about each template.
	* Use a trigger function to update the template count data whenever a user creates or deletes a template.
	* Create a policy to restrict access to template count data based on the user's role.
8. **Integrate with Lemon Squeezy:**
	* Use the Lemon Squeezy API to retrieve subscription data and display it in the Customer Portal.
	* Use the Lemon Squeezy API to retrieve usage data and display it in the Customer Portal.
9. **Integrate with Stripe:**
	* Use the Stripe API to retrieve payment data and display it in the billing page.
	* Use the Stripe API to retrieve invoice data and display it in the Customer Portal.

**What to Avoid:**

* Do not store sensitive data in plain text.
* Do not use hard-coded values for tier-specific data.
* Do not use a single policy for all tiers.

**Additional Tips:**

* Use a consistent naming convention for tables and columns.
* Use a consistent naming convention for policies and roles.
* Use a trigger function to update data whenever a user performs an action.
* Use a policy to restrict access to data based on the user's role.

**API Endpoints:**

* Supabase:
	+ `GET /subscriptions`: Retrieve subscription data for a customer.
	+ `GET /usage`: Retrieve usage data for a customer.
	+ `GET /invoices`: Retrieve invoice data for a customer.
	+ `GET /customers`: Retrieve customer data, including seat information.
	+ `GET /templates`: Retrieve template data, including template counts.
* Lemon Squeezy:
	+ `GET /subscriptions`: Retrieve subscription data for a customer.
	+ `GET /usage`: Retrieve usage data for a customer.
* Stripe:
	+ `GET /payments`: Retrieve payment data for a customer.
	+ `GET /invoices`: Retrieve invoice data for a customer.

## Notes per source

### https://docs.lemonsqueezy.com/help/online-store/customer-portal
Based on the provided documentation from Lemon Squeezy, here are some concrete, actionable, verifiable techniques for building tier-specific dashboards, usage meters, upgrade prompts, billing page, invoices, seat management, and template counts per plan:

1. **Tier-specific dashboards**:
	* Use the Customer Portal's customization feature to toggle different features and data shown to customers based on their plan tier.
	* Use the `Design settings` in the Lemon Squeezy dashboard to customize the Customer Portal.
2. **Usage meters**:
	* Use the `Usage` feature in Lemon Squeezy to track customer usage and display it in the Customer Portal.
	* Use the `API` to retrieve usage data and display it in the Customer Portal.
3. **Upgrade prompts**:
	* Use the `Subscription` feature in Lemon Squeezy to track customer subscriptions and display upgrade prompts based on their plan tier.
	* Use the `API` to retrieve subscription data and display upgrade prompts in the Customer Portal.
4. **Billing page**:
	* Use the Customer Portal's billing feature to display customer billing information.
	* Use the `API` to retrieve billing data and display it in the Customer Portal.
5. **Invoices**:
	* Use the `Invoices` feature in Lemon Squeezy to generate and display customer invoices.
	* Use the `API` to retrieve invoice data and display it in the Customer Portal.
6. **Seat management**:
	* Use the `Customers` feature in Lemon Squeezy to manage customer seats and display seat information in the Customer Portal.
	* Use the `API` to retrieve customer data and display seat information in the Customer Portal.
7. **Template counts per plan**:
	* Use the `Templates` feature in Lemon Squeezy to track template counts and display them in the Customer Portal based on the customer's plan tier.
	* Use the `API` to retrieve template data and display template counts in the Customer Portal.

To implement these features, you can use the following API endpoints:

* `GET /subscriptions`: Retrieve subscription data for a customer.
* `GET /usage`: Retrieve usage data for a customer.
* `GET /invoices`: Retrieve invoice data for a customer.
* `GET /customers`: Retrieve customer data, including seat information.
* `GET /templates`: Retrieve template data, including template counts.

You can also use the Customer Portal's customization feature to toggle different features and data shown to customers based on their plan tier.

Note that these are just some of the possible techniques for implementing these features, and you may need to modify them to fit your specific use case.

### https://supabase.com/docs/guides/database/postgres/row-level-security
Based on the Supabase documentation, here are the concrete, actionable, verifiable techniques to build tier-specific dashboards, usage meters, upgrade prompts, billing page, invoices, seat management, and template counts per plan:

**Tier-specific dashboards:**

1. Create separate tables for each tier (e.g., `starter`, `pro`, `team`, `scale`) to store tier-specific data.
2. Use Row Level Security (RLS) to restrict access to tier-specific data based on the user's role.
3. Create policies for each tier to control which data is visible to users with different roles.

**Usage meters:**

1. Create a `usage` table to store usage data for each user.
2. Use a trigger function to update the usage data whenever a user performs an action (e.g., creates a new template).
3. Create a policy to restrict access to usage data based on the user's role.

**Upgrade prompts:**

1. Create a `plans` table to store information about each plan (e.g., `starter`, `pro`, `team`, `scale`).
2. Use a trigger function to update the user's plan whenever they upgrade.
3. Create a policy to restrict access to plan information based on the user's role.

**Billing page:**

1. Create a `invoices` table to store invoice data for each user.
2. Use a trigger function to update the invoice data whenever a user is charged.
3. Create a policy to restrict access to invoice data based on the user's role.

**Seat management:**

1. Create a `seats` table to store information about each user's seats (e.g., number of users, number of templates).
2. Use a trigger function to update the seat data whenever a user is added or removed.
3. Create a policy to restrict access to seat data based on the user's role.

**Template counts per plan:**

1. Create a `templates` table to store information about each template.
2. Use a trigger function to update the template count data whenever a user creates or deletes a template.
3. Create a policy to restrict access to template count data based on the user's role.

Here is an example of how you might implement these techniques using Supabase:
```sql
-- Create tables for each tier
CREATE TABLE starter (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

CREATE TABLE pro (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

CREATE TABLE team (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

CREATE TABLE scale (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

-- Create usage table
CREATE TABLE usage (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

-- Create plans table
CREATE TABLE plans (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255),
  description TEXT
);

-- Create invoices table
CREATE TABLE invoices (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

-- Create seats table
CREATE TABLE seats (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

-- Create templates table
CREATE TABLE templates (
  id SERIAL PRIMARY KEY,
  user_id UUID REFERENCES auth.users,
  data JSONB
);

-- Create policies for each tier
CREATE POLICY "Starter can view their own data" ON starter FOR SELECT TO authenticated USING (user_id = auth.uid());
CREATE POLICY "Pro can view their own data" ON pro FOR SELECT TO authenticated USING (user_id = auth.uid());
CREATE POLICY "Team can view their own data" ON team FOR SELECT TO authenticated USING (user_id = auth.uid());
CREATE POLICY "Scale can view their own data" ON scale FOR SELECT TO authenticated USING (user_id = auth.uid());

-- Create policy for usage data
CREATE POLICY "Users can view their own usage data" ON usage FOR SELECT TO authenticated USING (user_id = auth.uid());

-- Create policy for plan information
CREATE POLICY "Users can view their own plan information" ON plans FOR SELECT TO authenticated USING (user_id = auth.uid());

-- Create policy for invoice data
CREATE POLICY "Users can view their
