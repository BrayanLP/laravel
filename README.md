For those wanting an all automated solution via gulp, here it is:

Use the gulp packages gulp-connect-php and laravel-elixir-browsersync2. The first starts up the php artisan serve and the other connects it to browserSync.

Install the packages:
npm install laravel-elixir-browsersync2 --save-dev
npm install gulp-connect-php --save-dev
Add the required lines to your gulpfile.js:
Code:

var elixir = require('laravel-elixir'),
    gulp = require('gulp');
var connectPHP = require('gulp-connect-php');
var BrowserSync = require('laravel-elixir-browsersync2');

elixir(function(mix) {
    mix.sass('app.scss');
});

elixir(function(mix) {
    connectPHP.server({
        base: './public',
        hostname: '0.0.0.0',
        port: 8000
    });
    BrowserSync.init();
    mix.BrowserSync(
    {
        proxy: 'localhost:8000',
        logPrefix       : "Laravel Eixir BrowserSync",
        logConnections  : false,
        reloadOnRestart : false,
        notify          : false
    });
});
Then - simply gulp.
Disclaimer: This might not work with the gulp watch, but there might be people with the answer to that.

There is also a line PHP server not started. Retrying... before the [Laravel Eixir BrowserSync] Proxying: http://localhost:8000. It belongs to gulp-connect-php when trying to check if the server is running.
