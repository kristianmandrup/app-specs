# Pages Overview

PropertiesController
  index - search_command.execute(Properties::SearchCommand.
  show - Property.by_title(id)

Properties::FavoritesController
  index - current_user.favorites
  show - current_user.favorite(id)

Properties::MapController
  index
  show

Properties::LocationController
  show

LandlordController
  Security: Only landlord has access!

UserController
  Security: Only User has access!

Landlord::PropertiesController < LandlordController
  index (management) - landlord properties management
  edit (update) - landlord edit property page

Landlord::Properties::LocationController < LandlordController
  edit (update)

Landlord::UsersController (registration)
  new - register (create)

Tenant::UsersController (registration)
  new - register (create)

User::MailsController < UserController
  index - show mails for any user

User::ThreadsController < UserController
  index - show threads for any user
  show (update, create, destroy) - single user thread

User::SessionsController
  new - login
  destroy - logout

User::PreferencesController
  show (home)
  edit (update)

(For later!!!  - BEGIN)
Tenant::Packages
  index
  show
  create
  destroy

Landlord::Packages
  index
  show
  create
  destroy
(END)

# Widgets Overview

Each page uses following main widgets:

* header - Bars::Header
* content - Content
* footer - Bars::Footer

## Header

* main_header - Bars::MainHeader
* sub_header - Bars::SubHeader

The main_header is the top part of the header:

* search_sentence - Search::Sentence
* results_counter - Search::ResultsCounter
* navigation - Navigation::Page

The sub_header is the bottom part of the header:

* item_actions    - Item::Actions
* view_navigation - Item::Navigation
* sorter          - Search::Sorter

### Search sentence

* search_property_sentence - Search::Property::Sentence

* Search::Property::PartOfSentence

* Search::Property::LocationSentence (edit, update)
* Search::Property::TypeSentence (edit, update)
* Search::Property::RoomsSentence (edit, update)
* Search::Property::CostSentence (edit, update)
* Search::Property::PeriodSentence (edit, update)
* Search::Property::RatingSentence (edit, update)
* Search::Property::RentabilitySentence (edit, update)

Each part can communicate to container widget about state change in order to be reflected in other parts of sentence if needed!

### Search results counter

* Search::Property::ResultsCounter

### Navigation

labels depend on the state of the User Session

* :rent_home - rent_home_url (redirect to registration) - if not Landlord user 
* :new_home  - new_home_url - if Landlord user and current_property is nil
* :manage_property  - manage_property_url(property) - if Landlord user and current_property is not nil

### Sub-header

#### Item Actions

ItemActions

* property_actions        - Item::Property::Actions < ItemActions
* property_filter_actions - List::Properties::FilterActions < ItemActions

#### Properties Navigation

Depending on the list (or item type) the relevant view navigation is shown.

Navigation

* properties_navigation     - Properties::Navigation < Item::Navigation (show)

#### Sorter

A sorter is used to sort a (results) list of similar items:

Depending on the list type, the relevant sorter is displayed.

List::Sorter

* properties_sorter             - List::Properties::Sorter < List::Sorter (edit)
* properties_management_sorter  - List::Properties::Management::Sorter < List::Properties::Sorter (edit)
* mails_sorter                  - List::Mails::Sorter < List::Sorter (edit)
* threads_sorter                - List::Threads::Sorter < List::Mails::Sorter (edit)

## Content

Contains the content of the page:

Many of the pages either displays a list of items or a single item:

* list/item - Content
* map  - Content::Map

### Content views

Content

* properties             - Properties < Content (index, show, edit, update)
* properties_management  - Properties::Management < Properties (index, update, destroy)
* mails                  - Mails < Content (index, show)
* favorites              - Favorites < Content (index, show, destroy)

* threads                - Threads < Content (index, show, edit, new, update, destroy)

## Map views

Content::Map

* properties_map  - Map::Properties < Content::Map (index, show)
* mails_map       - Map::Mails < Content::Map (index, show)
* favorites_map   - Map::Favorites < Map::Properties (index, show)

## Location views

Content::Location

* properties_location - Location::Properties < Content::Location (show, edit, update)

## User

* user_session - User::Session (show, edit, new, create, destroy)
* user_preferences - User::Preferences (edit, update)
* user_registration - User::Registration (new)

## Account

* account - Account (show, edit, update)

## Account::Packages

* account_package - Account::Package (index, show, new, create, edit, update, destroy)

## Box widgets

* Properties::Box (show, management, favorite)

Decorators::
* BoxDecorator
* Box::BigAreaDecorator < BoxDecorator
* Box::NormalAreaDecorator < BoxDecorator
* Box::SmallAreaDecorator < BoxDecorator

* Box::UpperDecorator 
* Box::MiddleDecorator 
* Box::LowerDecorator

* Box::NormalArea::UpperDecorator < Box::UpperDecorator (indicator, overlay, actions)
* Box::NormalArea::MiddleDecorator < Box::MiddleDecorator (sides)
* Box::NormalArea::LowerDecorator < Box::LowerDecorator (value, actions)

Box::BigArea::UpperDecorator < Box::UpperDecorator (icon, title)

Property boxes:

* Properties::BoxDecorator < Box::NormalAreaDecorator
* Properties::Box::UpperDecorator
* Properties::Box::MiddleDecorator
* Properties::Box::LowerDecorator

* Properties::Management::BoxDecorator < Properties::BoxDecorator
* Properties::Management::Box::UpperDecorator < Properties::Box::UpperDecorator
* Properties::Management::Box::MiddleDecorator < Properties::Box::MiddleDecorator
* Properties::Management::Box::LowerDecorator < Properties::Box::LowerDecorator

* Properties::Favorite::BoxDecorator < Properties::BoxDecorator
* Properties::Favorite::Box::UpperDecorator < Properties::Box::UpperDecorator
* Properties::Favorite::Box::LowerDecorator < Properties::Box::LowerDecorator

Contact boxes:

Box widgets::
* Profile::Box (show) - (for user or company)
* Profile::ContactBox (show)
* Profile::ContactOptionsBox (show)

Decorators::
* Profile::BoxDecorator < Box::SmallAreaDecorator
* Profile::ContactOptionsBox::Upper < Box::NormalAreaBox::UpperDecorator
* Profile::ContactOptionsBox::Middle < Box::NormalAreaBox::MiddleDecorator
* Profile::UserBoxDecorator < Profile::BoxDecorator
* Profile::CompanyBoxDecorator < Profile::BoxDecorator
* Profile::ContactBoxDecorator < < Box::SmallAreaDecorator

* Profile::ContactOptionsBoxDecorator < Box::NormalAreaDecorator

* Profile::ContactStatsBoxDecorator < Box::NormalAreaDecorator

* Profile::ContactDecorator
* Profile::ContactStatsDecorator < Profile::ContactDecorator

## Property page

### RentalCosts

Box widgets::
* Property::Costs::RentalCostsBox

Decorators::
* Property::Section::Costs::RentalCostsDecorator

### Period

Box widgets::
* Property::Period::CalendarBox
* Property::Period::DurationBox

Decorators::
* Property::PeriodDecorator

## Mail

Box widgets::
* Mail::BoxWidget (show) for system or property

Decorators::
* Mail::BoxDecorator < Mail::BoxDecorator
* Mail::System::BoxDecorator < Mail::BoxDecorator
* Mail::Property::BoxDecorator < Mail::BoxDecorator

## Cover

* company_ads - CompanyAds (index)
* quick_search - Search::Quick (edit)
* navigation - reuse Navigation::Page (fx :rent_home)
* featured_properties - Properties::Featured (index, show)

## Footer

* main_footer - Bars::MainHeader
* sub_footer - Bars::SubHeader

The main_footer is the top part of the footer:

* user_session - User::Session
* navigation_actions - Item::Property::Navigation::Actions
* user_preferences - User::Preferences

The sub_footer is the bottom part of the footer:

* company_info - Company::Info
* company_social_actions - Company::SocialActions

