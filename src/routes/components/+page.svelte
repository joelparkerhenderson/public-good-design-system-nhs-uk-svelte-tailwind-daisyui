<script lang="ts">
  import ActionLink from '$lib/components/action-link/ActionLink.svelte';
  import BackLink from '$lib/components/back-link/BackLink.svelte';
  import Breadcrumb from '$lib/components/breadcrumb/Breadcrumb.svelte';
  import Button from '$lib/components/button/Button.svelte';
  import Card from '$lib/components/card/Card.svelte';
  import CharacterCount from '$lib/components/character-count/CharacterCount.svelte';
  import Checkboxes from '$lib/components/checkboxes/Checkboxes.svelte';
  import ContentsList from '$lib/components/contents-list/ContentsList.svelte';
  import DateInput from '$lib/components/date-input/DateInput.svelte';
  import Details from '$lib/components/details/Details.svelte';
  import DoDontList from '$lib/components/do-dont-list/DoDontList.svelte';
  import ErrorMessage from '$lib/components/error-message/ErrorMessage.svelte';
  import ErrorSummary from '$lib/components/error-summary/ErrorSummary.svelte';
  import Fieldset from '$lib/components/fieldset/Fieldset.svelte';
  import Hint from '$lib/components/hint/Hint.svelte';
  import Images from '$lib/components/images/Images.svelte';
  import Input from '$lib/components/input/Input.svelte';
  import InsetText from '$lib/components/inset-text/InsetText.svelte';
  import Label from '$lib/components/label/Label.svelte';
  import NotificationBanner from '$lib/components/notification-banner/NotificationBanner.svelte';
  import Pagination from '$lib/components/pagination/Pagination.svelte';
  import Panel from '$lib/components/panel/Panel.svelte';
  import Radios from '$lib/components/radios/Radios.svelte';
  import Select from '$lib/components/select/Select.svelte';
  import SkipLink from '$lib/components/skip-link/SkipLink.svelte';
  import SummaryList from '$lib/components/summary-list/SummaryList.svelte';
  import Tables from '$lib/components/tables/Tables.svelte';
  import Tabs from '$lib/components/tabs/Tabs.svelte';
  import Tag from '$lib/components/tag/Tag.svelte';
  import TaskList from '$lib/components/task-list/TaskList.svelte';
  import Textarea from '$lib/components/textarea/Textarea.svelte';
  import WarningCallout from '$lib/components/warning-callout/WarningCallout.svelte';
  import Footer from '$lib/components/footer/Footer.svelte';
  import Header from '$lib/components/header/Header.svelte';
  import Hero from '$lib/components/hero/Hero.svelte';
</script>

<svelte:head>
  <title>Components - Public Good Design System</title>
</svelte:head>

<div class="container mx-auto px-4 py-8">
  <header class="mb-8">
    <h1 class="text-3xl font-bold text-primary mb-4">Component Library</h1>
    <p class="text-base-content/70 text-lg">
      Converted NHS UK Design System components for Public Good projects
    </p>
  </header>

  <!-- Navigation -->
  <nav class="mb-8">
    <div class="breadcrumbs text-sm">
      <ul>
        <li><a href="/">Home</a></li>
        <li>Components</li>
      </ul>
    </div>
  </nav>

  <!-- Components Grid -->
  <div class="grid gap-8">
    
    <!-- Action Link Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Action Link
        </h2>
        <p class="text-base-content/70 mb-4">
          A styled link component with arrow icon for navigation actions
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <ActionLink 
              text="Find a GP practice"
              href="#"
            />
            
            <ActionLink 
              html="<strong>Book</strong> a vaccine appointment"
              href="#"
            />
            
            <ActionLink 
              text="External resource"
              href="https://example.com"
              openInNewWindow={true}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Interactive</div>
        </div>
      </div>
    </section>

    <!-- Back Link Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Back Link
        </h2>
        <p class="text-base-content/70 mb-4">
          Navigation component for going back to previous pages or triggering back actions
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <BackLink href="/search" />
            <BackLink text="Return to search results" href="/search" />
            <BackLink element="button" text="Go back" />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Interactive</div>
        </div>
      </div>
    </section>

    <!-- Breadcrumb Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Breadcrumb
        </h2>
        <p class="text-base-content/70 mb-4">
          Navigation trail showing the user's location within the site hierarchy
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <Breadcrumb 
              items={[
                { text: 'Home', href: '/' },
                { text: 'Services', href: '/services' },
                { text: 'Find a GP' }
              ]}
            />
            
            <Breadcrumb 
              items={[
                { text: 'Home', href: '/' },
                { text: 'Health A-Z', href: '/conditions' },
                { text: 'Mental health', href: '/conditions/mental-health' },
                { text: 'Depression' }
              ]}
              collapseOnMobile={true}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Responsive</div>
        </div>
      </div>
    </section>

    <!-- Button Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Button
        </h2>
        <p class="text-base-content/70 mb-4">
          Interactive button component supporting multiple variants, elements, and states
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="flex flex-wrap gap-3">
            <Button text="Primary" />
            <Button text="Secondary" variant="secondary" />
            <Button text="Warning" variant="warning" />
            <Button text="As Link" href="#" />
            <Button text="Disabled" disabled={true} />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Interactive</div>
          <div class="badge badge-outline">Form</div>
          <div class="badge badge-outline">Multiple Variants</div>
        </div>
      </div>
    </section>

    <!-- Card Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Card
        </h2>
        <p class="text-base-content/70 mb-4">
          Versatile content container with support for images, different variants, and care card types
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="grid gap-3 md:grid-cols-2 lg:grid-cols-3">
            <Card 
              heading="Basic Card"
              description="Simple card with heading and description."
            />
            
            <Card 
              heading="Secondary Card"
              description="Card with secondary styling."
              secondary={true}
            />
            
            <Card 
              heading="Feature Card"
              description="Highlighted feature card."
              feature={true}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Content</div>
          <div class="badge badge-outline">Layout</div>
          <div class="badge badge-outline">Multiple Variants</div>
        </div>
      </div>
    </section>

    <!-- Character Count Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Character Count
        </h2>
        <p class="text-base-content/70 mb-4">
          Enhanced textarea with character or word counting and threshold warnings
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <div class="max-w-md">
            <CharacterCount 
              name="demo"
              label={{ text: "Tell us your feedback" }}
              hint={{ text: "Be specific about what you liked or didn't like." }}
              maxlength={100}
              rows={3}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Form</div>
          <div class="badge badge-outline">Interactive</div>
          <div class="badge badge-outline">Validation</div>
        </div>
      </div>
    </section>

    <!-- Checkboxes Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Checkboxes
        </h2>
        <p class="text-base-content/70 mb-4">
          Multi-select form input with support for hints, conditional content, and exclusive options
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <div class="max-w-md">
            <Checkboxes 
              name="demo-services"
              fieldset={{
                legend: { text: "Which services do you need?" }
              }}
              items={[
                { value: "gp", text: "GP appointment" },
                { value: "dentist", text: "Dentist" },
                { value: "optician", text: "Eye test" }
              ]}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Form</div>
          <div class="badge badge-outline">Multi-select</div>
          <div class="badge badge-outline">Conditional Content</div>
        </div>
      </div>
    </section>

    <!-- Contents List Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Contents List
        </h2>
        <p class="text-base-content/70 mb-4">
          Table of contents navigation for multi-page guides and documentation
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <div class="max-w-xs">
            <ContentsList 
              items={[
                { text: "Overview", href: "#overview" },
                { text: "Symptoms", href: "#symptoms", current: true },
                { text: "Treatment", href: "#treatment" }
              ]}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Guide</div>
        </div>
      </div>
    </section>

    <!-- Date Input Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Date Input
        </h2>
        <p class="text-base-content/70 mb-4">
          Three-field date input with day, month, and year for accessible date collection
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <div class="max-w-md">
            <DateInput 
              id="demo-date"
              fieldset={{
                legend: { text: "Date of birth" }
              }}
              hint={{
                text: "For example, 27 3 1985"
              }}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Form</div>
          <div class="badge badge-outline">Date</div>
          <div class="badge badge-outline">Accessible</div>
        </div>
      </div>
    </section>

    <!-- Details Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Details (Collapsible)
        </h2>
        <p class="text-base-content/70 mb-4">
          Expandable content sections for additional information and help content
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <div class="max-w-md">
            <Details 
              summaryText="Help with booking appointments"
              text="You can book appointments online through your GP practice's website, by calling them directly, or using the NHS App."
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Content</div>
          <div class="badge badge-outline">Collapsible</div>
          <div class="badge badge-outline">Help</div>
        </div>
      </div>
    </section>

    <!-- Do Don't List Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Do and Don't List
        </h2>
        <p class="text-base-content/70 mb-4">
          Guidance lists showing recommended and discouraged actions with clear visual indicators
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="grid gap-4 md:grid-cols-2">
            <DoDontList 
              title="Do"
              type="tick"
              headingLevel={4}
              items={[
                { item: "wash your hands regularly" },
                { item: "get plenty of rest" }
              ]}
            />
            
            <DoDontList 
              title="Don't"
              type="cross"
              headingLevel={4}
              items={[
                { item: "ignore symptoms" },
                { item: "share personal items" }
              ]}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Content</div>
          <div class="badge badge-outline">Guidance</div>
          <div class="badge badge-outline">Visual</div>
        </div>
      </div>
    </section>

    <!-- Error Message Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Error Message
        </h2>
        <p class="text-base-content/70 mb-4">
          Display validation error messages for form fields with screen reader support
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-2">
            <ErrorMessage text="Enter your full name" />
            <ErrorMessage html="Enter a valid email address, like <strong>name@example.com</strong>" />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Validation</div>
          <div class="badge badge-outline">Accessibility</div>
        </div>
      </div>
    </section>

    <!-- Error Summary Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Error Summary
        </h2>
        <p class="text-base-content/70 mb-4">
          Summarize validation errors at the top of a page with links to problem fields
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <ErrorSummary 
            errorList={[
              { text: "Enter your full name", href: "#full-name" },
              { text: "Enter a valid email address", href: "#email" },
              { text: "Select your date of birth", href: "#date-of-birth" }
            ]}
          />
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Validation</div>
          <div class="badge badge-outline">Navigation</div>
        </div>
      </div>
    </section>

    <!-- Fieldset Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Fieldset
        </h2>
        <p class="text-base-content/70 mb-4">
          Group related form controls together with an optional legend
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <Fieldset 
            legend={{ text: "Personal information" }}
          >
            <div class="space-y-3">
              <div class="form-control">
                <label class="label" for="fieldset-first-name">
                  <span class="label-text">First name</span>
                </label>
                <input id="fieldset-first-name" type="text" class="input input-bordered input-sm" />
              </div>
              <div class="form-control">
                <label class="label" for="fieldset-last-name">
                  <span class="label-text">Last name</span>
                </label>
                <input id="fieldset-last-name" type="text" class="input input-bordered input-sm" />
              </div>
            </div>
          </Fieldset>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Structure</div>
          <div class="badge badge-outline">Grouping</div>
        </div>
      </div>
    </section>

    <!-- Hint Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Hint
        </h2>
        <p class="text-base-content/70 mb-4">
          Provide helpful guidance text for form fields and other UI elements
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <div class="form-control">
              <label class="label" for="hint-email">
                <span class="label-text">Email address</span>
              </label>
              <Hint text="We'll use this to send you appointment confirmations" />
              <input id="hint-email" type="email" class="input input-bordered input-sm" />
            </div>

            <div class="form-control">
              <label class="label" for="hint-phone">
                <span class="label-text">Phone number</span>
              </label>
              <Hint html="For example <strong>07700 900 123</strong>" />
              <input id="hint-phone" type="tel" class="input input-bordered input-sm" />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Guidance</div>
          <div class="badge badge-outline">Help</div>
        </div>
      </div>
    </section>

    <!-- Images Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Images
        </h2>
        <p class="text-base-content/70 mb-4">
          Display images with optional captions and responsive image support
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="grid gap-4 md:grid-cols-2">
            <Images 
              src="https://via.placeholder.com/300x200/0284c7/ffffff?text=Basic+Image"
              alt="Example image without caption"
            />
            
            <Images 
              src="https://via.placeholder.com/300x200/059669/ffffff?text=With+Caption"
              alt="Example image with caption"
              caption="This image demonstrates the caption feature"
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Media</div>
          <div class="badge badge-outline">Responsive</div>
          <div class="badge badge-outline">Accessibility</div>
        </div>
      </div>
    </section>

    <!-- Input Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Input
        </h2>
        <p class="text-base-content/70 mb-4">
          Text input fields with labels, hints, error messages, and various input types
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3 max-w-sm">
            <Input 
              name="demo-name"
              label={{ text: "Full name" }}
            />
            
            <Input 
              name="demo-email"
              type="email"
              label={{ text: "Email address" }}
              hint={{ text: "We'll use this to contact you" }}
            />
            
            <Input 
              name="demo-phone"
              type="tel"
              label={{ text: "Phone number" }}
              prefix="+44"
              hint={{ text: "UK mobile number" }}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Validation</div>
          <div class="badge badge-outline">Input Types</div>
        </div>
      </div>
    </section>

    <!-- Inset Text Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Inset Text
        </h2>
        <p class="text-base-content/70 mb-4">
          Highlight important information that stands out from the main content
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <InsetText text="This is important information that stands out from the main content." />
          
          <InsetText html="You can use <strong>bold text</strong> and <em>links</em> in inset content." />
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Content</div>
          <div class="badge badge-outline">Information</div>
          <div class="badge badge-outline">Highlight</div>
        </div>
      </div>
    </section>

    <!-- Label Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Label
        </h2>
        <p class="text-base-content/70 mb-4">
          Accessible form labels that can be used standalone or as page headings
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3 max-w-sm">
            <Label text="Full name" for="demo-label-name" />
            <input type="text" id="demo-label-name" class="input input-bordered input-sm" />
            
            <Label html="Email <span class='text-error'>*</span>" for="demo-label-email" />
            <input type="email" id="demo-label-email" class="input input-bordered input-sm" />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Accessibility</div>
          <div class="badge badge-outline">Labels</div>
        </div>
      </div>
    </section>

    <!-- Notification Banner Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Notification Banner
        </h2>
        <p class="text-base-content/70 mb-4">
          Display important messages with different types and appropriate ARIA roles
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <NotificationBanner 
              type="success"
              text="Your appointment has been successfully booked."
            />
            
            <NotificationBanner 
              type="warning"
              titleText="Service disruption"
              text="Online booking will be unavailable for maintenance Sunday 2am-6am."
            />
            
            <NotificationBanner 
              type="info"
              text="You can now book COVID-19 vaccinations online."
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Alerts</div>
          <div class="badge badge-outline">Messages</div>
          <div class="badge badge-outline">Accessibility</div>
        </div>
      </div>
    </section>

    <!-- Pagination Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Pagination
        </h2>
        <p class="text-base-content/70 mb-4">
          Navigate between related pages in a series with clear previous/next links
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-4">
            <Pagination 
              previousUrl="#"
              previousPage="Understanding symptoms"
              nextUrl="#"
              nextPage="Treatment options"
            />
            
            <Pagination 
              nextUrl="#"
              nextPage="Getting started"
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Articles</div>
          <div class="badge badge-outline">Guides</div>
        </div>
      </div>
    </section>

    <!-- Panel Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Panel
        </h2>
        <p class="text-base-content/70 mb-4">
          Display important information in a prominent container with customizable headings
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-3">
            <Panel 
              titleText="Your appointment is confirmed"
              text="We've sent you a confirmation email with all the details."
            />
            
            <Panel 
              titleText="Registration complete"
              html="Welcome to our patient portal. You can now <strong>book appointments</strong> and view test results online."
              headingLevel={3}
            />
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Confirmations</div>
          <div class="badge badge-outline">Announcements</div>
          <div class="badge badge-outline">Prominent</div>
        </div>
      </div>
    </section>

    <!-- Radios Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Radios
        </h2>
        <p class="text-base-content/70 mb-4">
          Single-choice selection with hints, conditional content, and full accessibility
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Example:</h3>
          
          <Radios 
            name="demo-appointment"
            fieldset={{
              legend: { text: "What type of appointment do you need?" }
            }}
            items={[
              { text: "GP consultation", value: "gp" },
              { text: "Nurse appointment", value: "nurse" },
              { text: "Blood test", value: "blood-test" },
              { text: "Vaccination", value: "vaccination" }
            ]}
          />
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Selection</div>
          <div class="badge badge-outline">Conditional</div>
        </div>
      </div>
    </section>

    <!-- Select Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Select
        </h2>
        <p class="text-base-content/70 mb-4">
          Dropdown selection for choosing one option from a list with full form integration
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="space-y-3">
              <h4 class="font-medium">Basic Select</h4>
              <Select 
                name="demo-appointment-type"
                label={{ text: "Type of appointment" }}
                items={[
                  { text: "Choose an option", value: "" },
                  { text: "GP consultation", value: "gp" },
                  { text: "Nurse appointment", value: "nurse" },
                  { text: "Blood test", value: "blood-test" },
                  { text: "Vaccination", value: "vaccination" }
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">With Hint and Error</h4>
              <Select 
                name="demo-gp-selection"
                label={{ text: "Choose your GP" }}
                hint={{ text: "Select the doctor you'd like to see" }}
                errorMessage={{ text: "You must select a GP to continue" }}
                items={[
                  { text: "Please select a GP", value: "" },
                  { text: "Dr. Sarah Johnson", value: "dr-johnson" },
                  { text: "Dr. Michael Brown", value: "dr-brown" },
                  { text: "Dr. Emily Davis", value: "dr-davis" }
                ]}
              />
            </div>
            
            <div class="space-y-3 md:col-span-2">
              <h4 class="font-medium">Medical Specialties</h4>
              <Select 
                name="demo-specialty"
                label={{ text: "Which specialist do you need to see?" }}
                hint={{ text: "Choose the medical specialty for your referral" }}
                items={[
                  { text: "Choose a specialty", value: "" },
                  { text: "Cardiology (Heart)", value: "cardiology" },
                  { text: "Dermatology (Skin)", value: "dermatology" },
                  { text: "Neurology (Brain/Nervous System)", value: "neurology" },
                  { text: "Orthopedics (Bones/Joints)", value: "orthopedics" }
                ]}
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Forms</div>
          <div class="badge badge-outline">Dropdown</div>
          <div class="badge badge-outline">Selection</div>
        </div>
      </div>
    </section>

    <!-- Skip Link Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Skip Link
        </h2>
        <p class="text-base-content/70 mb-4">
          Keyboard navigation aid that allows users to bypass repetitive content and jump to main sections
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-4">
            <div class="alert alert-info">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" class="stroke-current shrink-0 w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
              </svg>
              <div>
                <h4 class="font-bold">How to see skip links</h4>
                <div class="text-sm">Press <kbd class="kbd kbd-sm">Tab</kbd> on this page to see skip links appear in the top-left corner</div>
              </div>
            </div>
            
            <div class="grid gap-4 md:grid-cols-2">
              <div class="space-y-3">
                <h4 class="font-medium">Basic Skip Link</h4>
                <div class="bg-base-200 p-4 rounded-lg relative min-h-20">
                  <SkipLink />
                  <p class="text-sm text-base-content/70">Default skip link (links to #maincontent)</p>
                </div>
              </div>
              
              <div class="space-y-3">
                <h4 class="font-medium">Custom Target</h4>
                <div class="bg-base-200 p-4 rounded-lg relative min-h-20">
                  <SkipLink 
                    text="Skip to emergency contacts"
                    href="#emergency"
                    classes="btn-error"
                  />
                  <p class="text-sm text-base-content/70">Emergency-focused with custom styling</p>
                </div>
              </div>
              
              <div class="space-y-3 md:col-span-2">
                <h4 class="font-medium">Healthcare Portal Skip Links</h4>
                <div class="bg-base-200 p-4 rounded-lg space-y-2">
                  <SkipLink text="Skip to appointment booking" href="#booking" />
                  <SkipLink text="Skip to test results" href="#results" />
                  <SkipLink text="Skip to prescriptions" href="#prescriptions" />
                  <p class="text-sm text-base-content/70">Multiple skip links for complex healthcare portals</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Accessibility</div>
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Keyboard</div>
        </div>
      </div>
    </section>

    <!-- Summary List Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Summary List
        </h2>
        <p class="text-base-content/70 mb-4">
          Display structured information as key-value pairs with optional edit/change actions
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="grid gap-4 md:grid-cols-2">
            <div class="space-y-3">
              <h4 class="font-medium">Basic Information</h4>
              <SummaryList 
                rows={[
                  {
                    key: { text: "Full name" },
                    value: { text: "Sarah Johnson" }
                  },
                  {
                    key: { text: "Date of birth" },
                    value: { text: "15 March 1985" }
                  },
                  {
                    key: { text: "NHS number" },
                    value: { text: "123 456 7890" }
                  }
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">With Actions</h4>
              <SummaryList 
                rows={[
                  {
                    key: { text: "Email address" },
                    value: { text: "sarah@email.com" },
                    actions: {
                      items: [
                        { 
                          href: "#change-email", 
                          text: "Change",
                          visuallyHiddenText: "email address"
                        }
                      ]
                    }
                  },
                  {
                    key: { text: "Phone number" },
                    value: { text: "07700 900 123" },
                    actions: {
                      items: [
                        { 
                          href: "#change-phone", 
                          text: "Change",
                          visuallyHiddenText: "phone number"
                        }
                      ]
                    }
                  }
                ]}
              />
            </div>
            
            <div class="space-y-3 md:col-span-2">
              <h4 class="font-medium">Test Results</h4>
              <SummaryList 
                rows={[
                  {
                    key: { text: "Blood pressure" },
                    value: { html: "<span class='text-success font-semibold'>120/80 mmHg</span><br>Normal range" }
                  },
                  {
                    key: { text: "Cholesterol" },
                    value: { html: "<span class='text-warning font-semibold'>5.2 mmol/L</span><br>Slightly elevated" }
                  },
                  {
                    key: { text: "Next review" },
                    value: { text: "6 months" },
                    actions: {
                      items: [
                        { 
                          href: "#book-review", 
                          text: "Book appointment",
                          visuallyHiddenText: "for follow-up review"
                        }
                      ]
                    }
                  }
                ]}
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Data Display</div>
          <div class="badge badge-outline">Actions</div>
          <div class="badge badge-outline">Healthcare</div>
        </div>
      </div>
    </section>

    <!-- Tables Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Tables
        </h2>
        <p class="text-base-content/70 mb-4">
          Display structured data in rows and columns with responsive layouts and accessibility features
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div class="space-y-3">
              <h4 class="font-medium">Basic Table</h4>
              <Tables 
                caption="Patient appointments"
                head={[
                  { text: "Time" },
                  { text: "Patient" },
                  { text: "Type" }
                ]}
                rows={[
                  [
                    { text: "9:00 AM" },
                    { text: "Sarah Johnson" },
                    { text: "GP consultation" }
                  ],
                  [
                    { text: "9:30 AM" },
                    { text: "Michael Brown" },
                    { text: "Blood test" }
                  ],
                  [
                    { text: "10:00 AM" },
                    { text: "Emily Davis" },
                    { text: "Vaccination" }
                  ]
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Test Results with Status</h4>
              <Tables 
                caption="Blood test results"
                head={[
                  { text: "Test" },
                  { text: "Result", format: "numeric" },
                  { text: "Range" },
                  { text: "Status" }
                ]}
                rows={[
                  [
                    { text: "Cholesterol" },
                    { text: "4.2", format: "numeric" },
                    { text: "< 5.0 mmol/L" },
                    { html: "<span class='badge badge-success'>Normal</span>" }
                  ],
                  [
                    { text: "Blood pressure" },
                    { text: "135/85", format: "numeric" },
                    { text: "< 140/90 mmHg" },
                    { html: "<span class='badge badge-warning'>Borderline</span>" }
                  ]
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Panel Table</h4>
              <Tables 
                panel={true}
                heading="Current vital signs"
                headingLevel={4}
                caption="Latest measurements"
                head={[
                  { text: "Measurement" },
                  { text: "Value", format: "numeric" },
                  { text: "Status" }
                ]}
                rows={[
                  [
                    { text: "Heart rate" },
                    { text: "72 bpm", format: "numeric" },
                    { html: "<span class='text-success'>Normal</span>" }
                  ],
                  [
                    { text: "Temperature" },
                    { text: "36.8°C", format: "numeric" },
                    { html: "<span class='text-success'>Normal</span>" }
                  ]
                ]}
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Data Display</div>
          <div class="badge badge-outline">Responsive</div>
          <div class="badge badge-outline">Healthcare</div>
        </div>
      </div>
    </section>

    <!-- Tabs Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Tabs
        </h2>
        <p class="text-base-content/70 mb-4">
          Organize content into accessible tab panels with keyboard navigation and mobile responsiveness
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div class="space-y-3">
              <h4 class="font-medium">Patient Information Tabs</h4>
              <Tabs 
                title="Patient dashboard"
                idPrefix="showcase-patient"
                items={[
                  {
                    label: "Overview",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">Patient Summary</h4>
                          <dl class="grid grid-cols-2 gap-2 text-sm">
                            <dt>Name:</dt>
                            <dd>Sarah Johnson</dd>
                            <dt>Age:</dt>
                            <dd>38 years</dd>
                            <dt>NHS Number:</dt>
                            <dd>123 456 7890</dd>
                            <dt>Status:</dt>
                            <dd><span class="badge badge-success badge-sm">Active</span></dd>
                          </dl>
                        </div>
                      `
                    }
                  },
                  {
                    label: "Medications",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">Current Prescriptions</h4>
                          <div class="space-y-2 text-sm">
                            <div class="flex justify-between items-center p-2 bg-base-50 rounded">
                              <span>Amlodipine 5mg</span>
                              <span class="badge badge-success badge-sm">Active</span>
                            </div>
                            <div class="flex justify-between items-center p-2 bg-base-50 rounded">
                              <span>Simvastatin 20mg</span>
                              <span class="badge badge-success badge-sm">Active</span>
                            </div>
                          </div>
                        </div>
                      `
                    }
                  },
                  {
                    label: "Results",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">Test Results</h4>
                          <div class="space-y-2 text-sm">
                            <div class="flex justify-between">
                              <span>Cholesterol:</span>
                              <span class="text-success font-semibold">4.2 mmol/L ✓</span>
                            </div>
                            <div class="flex justify-between">
                              <span>Blood Pressure:</span>
                              <span class="text-warning font-semibold">135/85 mmHg ⚠</span>
                            </div>
                          </div>
                        </div>
                      `
                    }
                  }
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Healthcare Services</h4>
              <Tabs 
                title="NHS services"
                idPrefix="showcase-services"
                items={[
                  {
                    label: "GP Services",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">General Practice</h4>
                          <ul class="text-sm space-y-1">
                            <li class="flex items-center gap-2">
                              <span class="badge badge-sm badge-success">✓</span>
                              General consultations
                            </li>
                            <li class="flex items-center gap-2">
                              <span class="badge badge-sm badge-success">✓</span>
                              Health checks and screening
                            </li>
                            <li class="flex items-center gap-2">
                              <span class="badge badge-sm badge-success">✓</span>
                              Vaccinations
                            </li>
                          </ul>
                        </div>
                      `
                    }
                  },
                  {
                    label: "Emergency",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">Emergency Services</h4>
                          <div class="alert alert-error alert-sm">
                            <span class="text-xs">Life-threatening emergency: Call 999</span>
                          </div>
                          <div class="text-sm">
                            <div class="flex justify-between">
                              <span>A&E wait time:</span>
                              <span class="badge badge-warning badge-sm">3-4 hours</span>
                            </div>
                          </div>
                        </div>
                      `
                    }
                  },
                  {
                    label: "Specialists",
                    panel: {
                      html: `
                        <div class="space-y-3">
                          <h4 class="font-semibold">Specialist Services</h4>
                          <div class="text-sm space-y-1">
                            <div class="flex justify-between">
                              <span>Cardiology:</span>
                              <span class="badge badge-warning badge-sm">8-12 weeks</span>
                            </div>
                            <div class="flex justify-between">
                              <span>Mental Health:</span>
                              <span class="badge badge-info badge-sm">2-6 weeks</span>
                            </div>
                          </div>
                        </div>
                      `
                    }
                  }
                ]}
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Keyboard Accessible</div>
          <div class="badge badge-outline">Mobile Responsive</div>
        </div>
      </div>
    </section>

    <!-- Tag Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Tag
        </h2>
        <p class="text-base-content/70 mb-4">
          Status indicator components for displaying the current state of items, processes, or tasks
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div class="space-y-3">
              <h4 class="font-medium">Appointment Status</h4>
              <div class="grid gap-4 md:grid-cols-2">
                <div class="card bg-base-50 border">
                  <div class="card-body">
                    <h5 class="font-semibold text-sm">Dr. Sarah Wilson - Cardiology</h5>
                    <p class="text-xs text-base-content/70">March 15, 2024 at 10:30 AM</p>
                    <div class="flex items-center gap-2 mt-2">
                      <Tag variant="green" text="Confirmed" />
                      <span class="text-xs text-base-content/50">Booked 2 days ago</span>
                    </div>
                  </div>
                </div>
                
                <div class="card bg-base-50 border">
                  <div class="card-body">
                    <h5 class="font-semibold text-sm">Dr. James Brown - General Practice</h5>
                    <p class="text-xs text-base-content/70">March 18, 2024 at 2:15 PM</p>
                    <div class="flex items-center gap-2 mt-2">
                      <Tag variant="blue" text="Pending" />
                      <span class="text-xs text-base-content/50">Awaiting confirmation</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Test Results Status</h4>
              <div class="space-y-2">
                <div class="flex justify-between items-center p-3 bg-base-50 rounded">
                  <div>
                    <span class="font-semibold text-sm">Blood Chemistry Panel</span>
                    <div class="text-xs text-base-content/70">March 10, 2024</div>
                  </div>
                  <Tag variant="green" text="Completed" />
                </div>
                
                <div class="flex justify-between items-center p-3 bg-base-50 rounded">
                  <div>
                    <span class="font-semibold text-sm">Chest X-Ray</span>
                    <div class="text-xs text-base-content/70">March 12, 2024</div>
                  </div>
                  <Tag variant="aqua-green" text="In Progress" />
                </div>
                
                <div class="flex justify-between items-center p-3 bg-base-50 rounded">
                  <div>
                    <span class="font-semibold text-sm">MRI Scan</span>
                    <div class="text-xs text-base-content/70">March 16, 2024</div>
                  </div>
                  <Tag variant="orange" text="Delayed" />
                </div>
              </div>
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">All Tag Variants</h4>
              <div class="grid gap-3 md:grid-cols-3">
                <div>
                  <h5 class="text-sm font-medium mb-2">Status</h5>
                  <div class="flex flex-wrap gap-1">
                    <Tag variant="green" text="Completed" />
                    <Tag variant="blue" text="Pending" />
                    <Tag variant="white" text="Started" />
                    <Tag variant="grey" text="Not Started" />
                  </div>
                </div>
                
                <div>
                  <h5 class="text-sm font-medium mb-2">Process</h5>
                  <div class="flex flex-wrap gap-1">
                    <Tag variant="purple" text="Under Review" />
                    <Tag variant="pink" text="Sent" />
                    <Tag variant="aqua-green" text="Active" />
                  </div>
                </div>
                
                <div>
                  <h5 class="text-sm font-medium mb-2">Priority</h5>
                  <div class="flex flex-wrap gap-1">
                    <Tag variant="red" text="Urgent" />
                    <Tag variant="orange" text="Important" />
                    <Tag variant="yellow" text="Review Due" />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Status Indicator</div>
          <div class="badge badge-outline">Accessible</div>
          <div class="badge badge-outline">Healthcare</div>
        </div>
      </div>
    </section>

    <!-- Task List Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Task List
        </h2>
        <p class="text-base-content/70 mb-4">
          Multi-step process components where users can complete tasks in any order with clear progress indication
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div class="space-y-3">
              <h4 class="font-medium">Patient Registration Process</h4>
              <p class="text-sm text-base-content/70">Complete your registration to access NHS services online. You can complete these tasks in any order.</p>
              
              <TaskList 
                items={[
                  {
                    title: "Personal details",
                    hint: "Provide your name, date of birth, and contact information",
                    href: "#personal-details",
                    status: {
                      text: "Completed",
                      variant: "completed"
                    }
                  },
                  {
                    title: "Medical history",
                    hint: "Tell us about any existing medical conditions",
                    href: "#medical-history", 
                    status: {
                      text: "Completed",
                      variant: "completed"
                    }
                  },
                  {
                    title: "Emergency contacts",
                    hint: "Add at least one emergency contact person",
                    href: "#emergency-contacts",
                    status: {
                      text: "In Progress",
                      variant: "in-progress"
                    }
                  },
                  {
                    title: "GP registration",
                    hint: "Confirm your current GP practice details",
                    href: "#gp-registration",
                    status: {
                      text: "Incomplete",
                      variant: "incomplete"
                    }
                  },
                  {
                    title: "Identity verification",
                    hint: "Upload a photo of your ID document",
                    status: {
                      text: "Cannot start yet",
                      variant: "cannot-start-yet"
                    }
                  }
                ]}
              />
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Appointment Booking Journey</h4>
              <p class="text-sm text-base-content/70">Book your appointment by completing the following steps.</p>
              
              <TaskList 
                items={[
                  {
                    title: "Choose appointment type",
                    hint: "Select the type of healthcare service you need",
                    href: "#appointment-type",
                    status: {
                      text: "Completed",
                      variant: "completed"
                    }
                  },
                  {
                    title: "Select healthcare provider",
                    hint: "Choose from available practices in your area",
                    href: "#select-provider",
                    status: {
                      text: "Completed", 
                      variant: "completed"
                    }
                  },
                  {
                    title: "Choose date and time",
                    hint: "Pick from available appointment slots",
                    href: "#choose-time",
                    status: {
                      text: "In Progress",
                      variant: "in-progress"
                    }
                  },
                  {
                    title: "Confirm booking",
                    hint: "Review and confirm your appointment details",
                    status: {
                      text: "Cannot start yet",
                      variant: "cannot-start-yet"
                    }
                  }
                ]}
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Multi-step Process</div>
          <div class="badge badge-outline">Progress Tracking</div>
          <div class="badge badge-outline">Accessible</div>
        </div>
      </div>
    </section>

    <!-- Textarea Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Textarea
        </h2>
        <p class="text-base-content/70 mb-4">
          Multi-line text input components for collecting longer responses with integrated labels, hints, and error messages
        </p>
        
        <div class="space-y-4">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div class="space-y-3">
              <h4 class="font-medium">Patient Symptom Description</h4>
              <div class="max-w-xl">
                <Textarea
                  name="symptoms-demo"
                  label={{
                    text: "Can you provide more detail about your symptoms?"
                  }}
                  hint={{
                    text: "Do not include personal information like your name or NHS number"
                  }}
                  rows={4}
                  placeholder="Describe when symptoms started and how they affect you..."
                />
              </div>
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Medical History Collection</h4>
              <div class="max-w-xl">
                <Textarea
                  name="medical-history-demo"
                  label={{
                    text: "List your current medications and health conditions"
                  }}
                  hint={{
                    text: "Include prescription drugs, over-the-counter medications, and dosages if known"
                  }}
                  rows={5}
                  required={true}
                />
              </div>
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Error State Example</h4>
              <div class="max-w-xl">
                <Textarea
                  name="error-demo"
                  label={{
                    text: "Why can't you provide a National Insurance number?"
                  }}
                  hint={{
                    text: "We need to understand your circumstances to help you"
                  }}
                  errorMessage={{
                    text: "You must provide an explanation"
                  }}
                  rows={4}
                />
              </div>
            </div>
            
            <div class="space-y-3">
              <h4 class="font-medium">Different Sizes</h4>
              <div class="grid gap-4 md:grid-cols-2">
                <div>
                  <h5 class="text-sm font-medium mb-2">Compact (3 rows)</h5>
                  <Textarea
                    name="compact-demo"
                    label={{
                      text: "Brief description"
                    }}
                    hint={{
                      text: "Keep response short and focused"
                    }}
                    rows={3}
                  />
                </div>
                
                <div>
                  <h5 class="text-sm font-medium mb-2">Extended (8 rows)</h5>
                  <Textarea
                    name="extended-demo"
                    label={{
                      text: "Detailed explanation"
                    }}
                    hint={{
                      text: "Provide comprehensive information"
                    }}
                    rows={8}
                  />
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Multi-line Input</div>
          <div class="badge badge-outline">Form Integration</div>
          <div class="badge badge-outline">Accessible</div>
        </div>
      </div>
    </section>

    <!-- Warning Callout Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Warning Callout
        </h2>
        <p class="text-base-content/70 mb-4">
          Critical health information callouts with distinctive yellow styling for highlighting time-sensitive or important health guidance
        </p>
        
        <div class="space-y-6">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div>
              <h4 class="font-medium mb-3">Default Warning Callout</h4>
              <WarningCallout text="This is important information that users need to be aware of for their health and safety." />
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Medication Alert</h4>
              <WarningCallout 
                heading="Medication Alert" 
                text="Always check with your healthcare provider before stopping any medication, even if you feel better."
              />
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Emergency Information</h4>
              <WarningCallout 
                headingLevel={2}
                heading="Emergency Contact"
                text="If this is a medical emergency, call 999 immediately. Do not wait to seek emergency care."
              />
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Complex Health Information</h4>
              <WarningCallout heading="Mental Health Support">
                <p>If you're feeling overwhelmed or having thoughts of self-harm:</p>
                <ul class="list-disc pl-6 mt-2">
                  <li>Call the Samaritans free on 116 123 (24/7)</li>
                  <li>Visit your local emergency department</li>
                  <li>Call 999 if you're in immediate danger</li>
                </ul>
                <p class="mt-3">Remember: <strong>You are not alone</strong>, and help is available.</p>
              </WarningCallout>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Time-Sensitive Health Information</h4>
              <WarningCallout 
                heading="Stroke Symptoms - Act F.A.S.T"
                html="<p>If you notice any of these signs, call 999 immediately:</p>
                <ul class='list-none mt-2 space-y-1'>
                  <li><strong>F</strong>ace - Has their face dropped on one side?</li>
                  <li><strong>A</strong>rms - Can they raise both arms above their head?</li>
                  <li><strong>S</strong>peech - Is their speech slurred?</li>
                  <li><strong>T</strong>ime - Time to call 999 if you see any of these signs</li>
                </ul>"
              />
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Critical Information</div>
          <div class="badge badge-outline">Health Guidance</div>
          <div class="badge badge-outline">Accessible</div>
        </div>
      </div>
    </section>

    <!-- Footer Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Footer
        </h2>
        <p class="text-base-content/70 mb-4">
          Consistent bottom-of-page navigation and copyright information for health services, following NHS UK design patterns
        </p>
        
        <div class="space-y-6">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div>
              <h4 class="font-medium mb-3">Standard Footer</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-b border-base-300">
                  Page content area
                </div>
                <Footer 
                  links={[
                    { text: 'Accessibility statement', href: '/accessibility-statement' },
                    { text: 'Contact us', href: '/contact' },
                    { text: 'Privacy policy', href: '/privacy' },
                    { text: 'Terms and conditions', href: '/terms' }
                  ]}
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Healthcare Service Footer</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-b border-base-300">
                  Healthcare service content
                </div>
                <Footer 
                  links={[
                    { text: 'Find NHS services', href: '/find-services' },
                    { text: 'Emergency contacts', href: '/emergency' },
                    { text: 'Patient support', href: '/patient-support' },
                    { text: 'Privacy policy', href: '/privacy' }
                  ]}
                  copyright="© NHS Digital"
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Minimal Footer</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-b border-base-300">
                  Simple service content
                </div>
                <Footer copyright="© 2024 Public Health Initiative" />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Extended Links Footer</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-b border-base-300">
                  Comprehensive service content  
                </div>
                <Footer 
                  links={[
                    { text: 'About this service', href: '/about' },
                    { text: 'Find NHS services', href: '/find-services' },
                    { text: 'Book appointments', href: '/appointments' },
                    { text: 'Patient support', href: '/patient-support' },
                    { text: 'Emergency contacts', href: '/emergency' },
                    { text: 'Accessibility statement', href: '/accessibility-statement' },
                    { text: 'Privacy policy', href: '/privacy' }
                  ]}
                  copyright="© Public Good Design System"
                />
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Page Footer</div>
          <div class="badge badge-outline">NHS Pattern</div>
          <div class="badge badge-outline">Accessible</div>
        </div>
      </div>
    </section>

    <!-- Header Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Header
        </h2>
        <p class="text-base-content/70 mb-4">
          Consistent top-of-page branding, navigation, and search functionality for health services, following NHS UK design patterns
        </p>
        
        <div class="space-y-6">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div>
              <h4 class="font-medium mb-3">Basic Header</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Header />
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-t border-base-300">
                  Page content area
                </div>
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Service Header</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Header 
                  serviceName="Book a COVID-19 vaccination"
                  serviceUrl="/book-vaccination"
                />
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-t border-base-300">
                  Service-specific content
                </div>
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Header with Navigation</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Header 
                  showNavigation={true}
                  navigationItems={[
                    { text: 'Health A-Z', href: '/health-a-z' },
                    { text: 'Services', href: '/services' },
                    { text: 'Live Well', href: '/live-well' },
                    { text: 'Mental Health', href: '/mental-health' }
                  ]}
                />
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-t border-base-300">
                  Content with primary navigation
                </div>
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Complete Service Header</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Header 
                  serviceName="Mental Health Support Service"
                  serviceUrl="/mental-health"
                  showNavigation={true}
                  navigationItems={[
                    { text: 'Book Appointment', href: '/book' },
                    { text: 'Manage Booking', href: '/manage' },
                    { text: 'Find Services', href: '/find' },
                    { text: 'Help', href: '/help' }
                  ]}
                  showSearch={true}
                  searchPlaceholder="Search support resources"
                />
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-t border-base-300">
                  Full-featured service with navigation and search
                </div>
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Transactional Header</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Header 
                  transactional={true}
                  serviceName="Complete Your Appointment"
                />
                <div class="bg-base-100 p-4 text-center text-base-content/50 text-sm border-t border-base-300">
                  Focused process - no distracting navigation
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Page Header</div>
          <div class="badge badge-outline">Navigation</div>
          <div class="badge badge-outline">Responsive</div>
        </div>
      </div>
    </section>

    <!-- Hero Section -->
    <section class="card bg-base-100 shadow-xl">
      <div class="card-body">
        <h2 class="card-title text-primary flex items-center gap-2">
          <div class="badge badge-success">✓ Converted</div>
          Hero
        </h2>
        <p class="text-base-content/70 mb-4">
          Prominent page introductions with headings, supporting text, and call-to-action buttons for health services
        </p>
        
        <div class="space-y-6">
          <h3 class="font-semibold">Examples:</h3>
          
          <div class="space-y-6">
            <div>
              <h4 class="font-medium mb-3">Basic Hero</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Hero 
                  heading="We're here for you"
                  text="Helping you take control of your health and wellbeing"
                  minHeight="min-h-48"
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Hero with Actions</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Hero 
                  heading="Access Your Health Records"
                  text="View test results, book appointments, and manage your healthcare online"
                  actions={[
                    { text: 'Find Services', href: '/services' },
                    { text: 'Book Appointment', href: '/book', variant: 'secondary' }
                  ]}
                  minHeight="min-h-56"
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Emergency Hero</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Hero 
                  variant="emergency"
                  heading="Emergency Care"
                  text="If this is a life-threatening emergency, call 999 immediately"
                  actions={[
                    { text: 'Call 999', href: 'tel:999' },
                    { text: 'Find Hospital', href: '/hospital', variant: 'outline' }
                  ]}
                  minHeight="min-h-48"
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Mental Health Support Hero</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Hero 
                  variant="info"
                  heading="Mental Health Support"
                  html="<p>You don't have to face mental health challenges alone.</p><p><strong>Free, confidential support is available 24/7.</strong></p>"
                  actions={[
                    { text: 'Get Help Now', href: '/mental-health' },
                    { text: 'Crisis Support', href: '/crisis', variant: 'secondary' }
                  ]}
                  minHeight="min-h-56"
                />
              </div>
            </div>
            
            <div>
              <h4 class="font-medium mb-3">Service Success Hero</h4>
              <div class="border border-base-300 rounded-lg overflow-hidden">
                <Hero 
                  variant="success"
                  heading="New Online Prescription Service"
                  text="Order repeat prescriptions online and collect from your local pharmacy"
                  actions={[
                    { text: 'Get Started', href: '/register' },
                    { text: 'Learn More', href: '/about', variant: 'outline' }
                  ]}
                  textAlign="left"
                  minHeight="min-h-48"
                />
              </div>
            </div>
          </div>
        </div>

        <div class="card-actions justify-end mt-4">
          <div class="badge badge-outline">Page Hero</div>
          <div class="badge badge-outline">Call to Action</div>
          <div class="badge badge-outline">Healthcare</div>
        </div>
      </div>
    </section>

    <!-- Completion Section -->
    <section class="card bg-base-200/50">
      <div class="card-body">
        <h2 class="card-title text-success flex items-center gap-2">
          <div class="badge badge-success">✅ Complete</div>
          All Components Converted
        </h2>
        <p class="text-success">
          🎉 Successfully converted all 35 NHS UK Design System components to Public Good Design System!
        </p>
        <div class="progress progress-primary w-full max-w-xs">
          <div class="bg-success" style="width: 100%"></div>
        </div>
        <div class="text-sm text-base-content/50">
          Progress: 35 of 35 components completed (100%)
        </div>
      </div>
    </section>

  </div>
</div>