# Menta Documentation

## Getting started

1.  Get selenium server from http://seleniumhq.org/download/ and run it

        java -jar selenium-server-standalone-2.13.0.jar

2.  Get php-webdriver and Menta

        git clone git://github.com/AOEmedia/php-webdriver.git php-webdriver
        git clone git://github.com/AOEmedia/Menta.git Menta

3.  If your selenium server runs on a different machine go to phpunit.xml and adapt the testing.selenium.seleniumServerUrl setting
(Or copy the phpunit.xml to foo.xml and run following command with --configuration=foo.xml)

4.  Run the sample test:

        cd Menta/Demo
        phpunit MentaDemoTest.php

## Setting up a test folder structure

### Bootstrapping and Autoloading

## Testcases

## Configuration handling

default.xml vs. phpunit xml configuration

## Components

### Organization of components

Project specific components
Component library (plattform specific, agency specific)
Rewrite mechanism to refine/override

### Rewrites

### Translations using __()

## Helpers

### Menta_Component_Helper_Common
### Menta_Component_Helper_Assert
### Menta_Component_Helper_Wait
### Menta_Component_Helper_Screenshot

## Event/Observers

## Configurations

## Session management

### Reuse browser sessions

### Setting up the session

## Screenshots

## PHPUnit

### Base classes

Selenium1 extends Selenium2 extends PHPUnit

### Running Tests

	cd /var/www
	git clone --recursive git@git.aoesupport.com:users/fabrizio.branca/TestSkeleton.git

	cd /var/www/TestSkeleton
	./composer.phar install

	cd /var/www/TestSkeleton/Tests
	mkdir -p ../../build/reports

	# Run single test
	../vendor/bin/phpunit -c ../conf/devfb.ff.vmhost.xml General/ScreenshotsTest.php

	# Run all tests
	../vendor/bin/phpunit -c ../conf/devfb.ff.vmhost.xml ../vendor/aoemedia/menta/lib/Menta/Util/CreateTestSuite.php

	# Report will be in /var/www/build/reports

### HTML Report

### Integration in Jenkins

### Text Result

## Sauce Labs

### Running on Sauce Labs

### Reporting test results to Sauce Labs

	/**
	 * Will send the test result to sauce labs in case we're running tests there
	 *
	 * @return void
	 */
	protected function tearDown() {

		$sauceUserId = $this->getConfiguration()->getValue('testing.sauce.userId');
		$sauceAccessKey = $this->getConfiguration()->getValue('testing.sauce.accessKey');

		if (!empty($sauceUserId) && !empty($sauceAccessKey) && Menta_SessionManager::activeSessionExists()) {
			$status = $this->getStatus();
			$passed = !($status == PHPUnit_Runner_BaseTestRunner::STATUS_ERROR || $status == PHPUnit_Runner_BaseTestRunner::STATUS_FAILURE);
			$rest = new WebDriver\SauceLabs\SauceRest($sauceUserId, $sauceAccessKey);
			$rest->updateJob(Menta_SessionManager::getSessionId(), array(WebDriver\SauceLabs\Capability::PASSED => $passed));
		}

		parent::tearDown();
	}

![Alt text](Documentation/aoemedia-new_rgb_72dpi.jpg)