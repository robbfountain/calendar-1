
## About Voidfire Calendar
A complete Laravel Nova Ant Vue Calendar Card Ready to work out of the box
![Laravel Nova Agenda](https://raw.githubusercontent.com/horaceho/laravel-nova-agenda/master/resources/images/nova-ant-design-vue.png)

## Getting Started
Requirements
- [Laravel](https://laravel.com/docs/master)
- [Laravel Nova](https://nova.laravel.com/docs/)

##  QuickStart
````
composer require voidfire/calendar
````
````
php artisan vendor:publish --tag=events-manager-migrations --force php artisan migrate
````

To setup the card, you must register the card with Nova. This is typically done in the `cards` method of the `NovaServiceProvider`.

```php
// in app/Providers/NovaServiceProvider.php


public function cards()
{
    return [
        // ...
        new \Voidfire\Calendar\Calendar,
    ];
}
```
<style>.bmc-button img{width: 35px !important;margin-bottom: 1px !important;box-shadow: none !important;border: none !important;vertical-align: middle !important;}.bmc-button{padding: 7px 10px 7px 10px !important;line-height: 35px !important;height:51px !important;min-width:217px !important;text-decoration: none !important;display:inline-flex !important;color:#FFFFFF !important;background-color:#FF813F !important;border-radius: 5px !important;border: 1px solid transparent !important;padding: 7px 10px 7px 10px !important;font-size: 22px !important;letter-spacing: 0.6px !important;box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;margin: 0 auto !important;font-family:'Cookie', cursive !important;-webkit-box-sizing: border-box !important;box-sizing: border-box !important;-o-transition: 0.3s all linear !important;-webkit-transition: 0.3s all linear !important;-moz-transition: 0.3s all linear !important;-ms-transition: 0.3s all linear !important;transition: 0.3s all linear !important;}.bmc-button:hover, .bmc-button:active, .bmc-button:focus {-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;text-decoration: none !important;box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;opacity: 0.85 !important;color:#FFFFFF !important;}</style><link href="https://fonts.googleapis.com/css?family=Cookie" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/GTUvX9O"><img src="https://cdn.buymeacoffee.com/buttons/bmc-new-btn-logo.svg" alt="Buy me a coffee"><span style="margin-left:15px;font-size:28px !important;">Buy me a coffee</span></a>

The package will create for you the needed entities for the calendar Events
````
````
````create_events_table.php```` migration file:
````
    public function up()
    {
        Schema::create('events', function (Blueprint $table) {
            $table->increments('id');
            $table->text('title');
            $table->dateTime('start_date')->nullable();
            $table->dateTime('end_date')->nullable();
            $table->timestamps();
        });
    }
````

````
````
````App\Nova\Event.php```` resource:
````
    public function fields(Request $request)
    {
        return [
            ID::make()->sortable(),
            Text::make('Title')->rules('required'),
            DateTime::make('From', 'start_date'),
            DateTime::make('To', 'end_date'),
        ];
    }
````
 ````App\Event.php```` model:
````
class Event extends Model
{
    protected $dates = [
        'start_date',
        'end_date',
    ];
}
````

