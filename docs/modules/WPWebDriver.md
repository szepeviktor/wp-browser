# WPBrowser module
This module should be used in acceptance tests, see [levels of testing for more information](./../levels-of-testing.md).  
This module extends the [WebDriver module](https://codeception.com/docs/modules/WebDriver) adding WordPress-specific configuration parameters and methods.  
The module simulates a user interaction with the site **with Javascript support**; if you don't need to test your project with Javascript support use the [WPBrowser module](WPBrowser.md).  
<!--doc-->


## Public API
<nav>
	<ul>
		<li>
			<a href="#activateplugin">activatePlugin</a>
		</li>
		<li>
			<a href="#ameditingpostwithid">amEditingPostWithId</a>
		</li>
		<li>
			<a href="#amonadminajaxpage">amOnAdminAjaxPage</a>
		</li>
		<li>
			<a href="#amonadminpage">amOnAdminPage</a>
		</li>
		<li>
			<a href="#amoncronpage">amOnCronPage</a>
		</li>
		<li>
			<a href="#amonpagespage">amOnPagesPage</a>
		</li>
		<li>
			<a href="#amonpluginspage">amOnPluginsPage</a>
		</li>
		<li>
			<a href="#deactivateplugin">deactivatePlugin</a>
		</li>
		<li>
			<a href="#dontseeplugininstalled">dontSeePluginInstalled</a>
		</li>
		<li>
			<a href="#grabcookieswithpattern">grabCookiesWithPattern</a>
		</li>
		<li>
			<a href="#grabfullurl">grabFullUrl</a>
		</li>
		<li>
			<a href="#grabwordpresstestcookie">grabWordPressTestCookie</a>
		</li>
		<li>
			<a href="#loginas">loginAs</a>
		</li>
		<li>
			<a href="#loginasadmin">loginAsAdmin</a>
		</li>
		<li>
			<a href="#seeerrormessage">seeErrorMessage</a>
		</li>
		<li>
			<a href="#seemessage">seeMessage</a>
		</li>
		<li>
			<a href="#seepluginactivated">seePluginActivated</a>
		</li>
		<li>
			<a href="#seeplugindeactivated">seePluginDeactivated</a>
		</li>
		<li>
			<a href="#seeplugininstalled">seePluginInstalled</a>
		</li>
		<li>
			<a href="#seewpdiepage">seeWpDiePage</a>
		</li>
		<li>
			<a href="#waitforjqueryajax">waitForJqueryAjax</a>
		</li>
	</ul>
</nav>

<h3>activatePlugin</h3>

<hr>

<p>In the plugin administration screen activates one or more plugins clicking the &quot;Activate&quot; link. The method will <strong>not</strong> handle authentication and navigation to the plugins administration page.</p>
<pre><code class="language-php">    // Activate a plugin.
    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;activatePlugin('hello-dolly');
    // Activate a list of plugins.
    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;activatePlugin(['hello-dolly','another-plugin']);</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string/array</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot; or a list of plugin slugs.</li></ul>
  

<h3>amEditingPostWithId</h3>

<hr>

<p>Go to the admin page to edit the post with the specified ID. The method will <strong>not</strong> handle authentication the admin area.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $postId = $I-&gt;havePostInDatabase();
    $I-&gt;amEditingPostWithId($postId);
    $I-&gt;fillField('post_title', 'Post title');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>int</code> <strong>$id</strong> - The post ID.</li></ul>
  

<h3>amOnAdminAjaxPage</h3>

<hr>

<p>Go to the <code>admin-ajax.php</code> page to start a synchronous, and blocking, <code>GET</code> AJAX request. The method will <strong>not</strong> handle authentication, nonces or authorization.</p>
<pre><code class="language-php">    $I-&gt;amOnAdminAjaxPage(['action' =&gt; 'my-action', 'data' =&gt; ['id' =&gt; 23], 'nonce' =&gt; $nonce]);</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>array/string</code> <strong>$queryVars</strong> - A string or array of query variables to append to the AJAX path.</li></ul>
  

<h3>amOnAdminPage</h3>

<hr>

<p>Go to a page in the admininstration area of the site. This method will <strong>not</strong> handle authentication to the administration area.</p>
<pre><code class="language-php">    $I-&gt;loginAs('user', 'password');
    // Go to the plugins management screen.
    $I-&gt;amOnAdminPage('/plugins.php');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$page</strong> - The path, relative to the admin area URL, to the page.</li></ul>
  

<h3>amOnCronPage</h3>

<hr>

<p>Go to the cron page to start a synchronous, and blocking, <code>GET</code> request to the cron script.</p>
<pre><code class="language-php">    // Triggers the cron job with an optional query argument.
    $I-&gt;amOnCronPage('/?some-query-var=some-value');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>array/string</code> <strong>$queryVars</strong> - A string or array of query variables to append to the AJAX path.</li></ul>
  

<h3>amOnPagesPage</h3>

<hr>

<p>Go the &quot;Pages&quot; administration screen. The method will <strong>not</strong> handle authentication.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPagesPage();
    $I-&gt;see('Add New');</code></pre>
  

<h3>amOnPluginsPage</h3>

<hr>

<p>Go to the plugins administration screen. The method will <strong>not</strong> handle authentication.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;activatePlugin('hello-dolly');</code></pre>
  

<h3>deactivatePlugin</h3>

<hr>

<p>In the plugin administration screen deactivate a plugin clicking the &quot;Deactivate&quot; link. The method will <strong>not</strong> handle authentication and navigation to the plugins administration page.</p>
<pre><code class="language-php">    // Deactivate one plugin.
    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;deactivatePlugin('hello-dolly');
    // Deactivate a list of plugins.
    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;deactivatePlugin(['hello-dolly', 'my-plugin']);</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string/array</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot;, or a list of plugin slugs.</li></ul>
  

<h3>dontSeePluginInstalled</h3>

<hr>

<p>Assert a plugin is not installed in the plugins administration screen. The method will <strong>not</strong> handle authentication and navigation to the plugin administration screen.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;dontSeePluginInstalled('my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot;.</li></ul>
  

<h3>grabCookiesWithPattern</h3>

<hr>

<p>Returns all the cookies whose name matches a regex pattern.</p>
<pre><code class="language-php">    $I-&gt;loginAs('customer','password');
    $I-&gt;amOnPage('/shop');
    $cartCookies = $I-&gt;grabCookiesWithPattern("#^shop_cart\\.*#");</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$cookiePattern</strong> - The regular expression pattern to use for the matching.</li></ul>
  

<h3>grabFullUrl</h3>

<hr>

<p>Grabs the current page full URL including the query vars.</p>
<pre><code class="language-php">    $today = date('Y-m-d');
    $I-&gt;amOnPage('/concerts?date=' . $today);
    $I-&gt;assertRegExp('#\\/concerts$#', $I-&gt;grabFullUrl());</code></pre>
  

<h3>grabWordPressTestCookie</h3>

<hr>

<p>Returns WordPress default test cookie object if present.</p>
<pre><code class="language-php">    // Grab the default WordPress test cookie.
    $wpTestCookie = $I-&gt;grabWordPressTestCookie();
    // Grab a customized version of the test cookie.
    $myTestCookie = $I-&gt;grabWordPressTestCookie('my_test_cookie');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$name</strong> - Optional, overrides the default cookie name.</li></ul>
  

<h3>loginAs</h3>

<hr>

<p>Login as the specified user. The method will <strong>not</strong> follow redirection, after the login, to any page. Depending on the driven browser the login might be &quot;too fast&quot; and the server might have not replied with valid cookies yet; in that case the method will re-attempt the login to obtain the cookies.</p>
<pre><code class="language-php">    $I-&gt;loginAs('user', 'password');
    $I-&gt;amOnAdminPage('/');
    $I-&gt;see('Dashboard');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$username</strong> - The user login name.</li>
<li><code>string</code> <strong>$password</strong> - The user password in plain text.</li>
<li><code>int</code> <strong>$timeout</strong> - The max time, in seconds, to try to login.</li>
<li><code>int</code> <strong>$maxAttempts</strong> - The max number of attempts to try to login.</li></ul>
  

<h3>loginAsAdmin</h3>

<hr>

<p>Login as the administrator user using the credentials specified in the module configuration. The method will <strong>not</strong> follow redirection, after the login, to any page.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnAdminPage('/');
    $I-&gt;see('Dashboard');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>int</code> <strong>$timeout</strong> - The max time, in seconds, to try to login.</li>
<li><code>int</code> <strong>$maxAttempts</strong> - The max number of attempts to try to login.</li></ul>
  

<h3>seeErrorMessage</h3>

<hr>

<p>In an administration screen look for an error admin notice. The check is class-based to decouple from internationalization. The method will <strong>not</strong> handle authentication and navigation the administration area.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin()ja
    $I-&gt;amOnAdminPage('/');
    $I-&gt;seeErrorMessage('.my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string/array/string</code> <strong>$classes</strong> - A list of classes the notice should have other than the <code>.notice.notice-error</code> ones.</li></ul>
  

<h3>seeMessage</h3>

<hr>

<p>In an administration screen look for an admin notice. The check is class-based to decouple from internationalization. The method will <strong>not</strong> handle authentication and navigation the administration area.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin()ja
    $I-&gt;amOnAdminPage('/');
    $I-&gt;seeMessage('.missing-api-token.my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string/array/string</code> <strong>$classes</strong> - A list of classes the message should have in addition to the <code>.notice</code> one.</li></ul>
  

<h3>seePluginActivated</h3>

<hr>

<p>Assert a plugin is activated in the plugin administration screen. The method will <strong>not</strong> handle authentication and navigation to the plugin administration screen.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;seePluginActivated('my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot;.</li></ul>
  

<h3>seePluginDeactivated</h3>

<hr>

<p>Assert a plugin is not activated in the plugins administration screen. The method will <strong>not</strong> handle authentication and navigation to the plugin administration screen.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;seePluginDeactivated('my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot;.</li></ul>
  

<h3>seePluginInstalled</h3>

<hr>

<p>Assert a plugin is installed, no matter its activation status, in the plugin adminstration screen. The method will <strong>not</strong> handle authentication and navigation to the plugin administration screen.</p>
<pre><code class="language-php">    $I-&gt;loginAsAdmin();
    $I-&gt;amOnPluginsPage();
    $I-&gt;seePluginInstalled('my-plugin');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>string</code> <strong>$pluginSlug</strong> - The plugin slug, like &quot;hello-dolly&quot;.</li></ul>
  

<h3>seeWpDiePage</h3>

<hr>

<p>Checks that the current page is one generated by the <code>wp_die</code> function. The method will try to identify the page based on the default WordPress die page HTML attributes.</p>
<pre><code class="language-php">    $I-&gt;loginAs('user', 'password');
    $I-&gt;amOnAdminPage('/forbidden');
    $I-&gt;seeWpDiePage();</code></pre>
  

<h3>waitForJqueryAjax</h3>

<hr>

<p>Waits for any jQuery triggered AJAX request to be resolved.</p>
<pre><code class="language-php">    $I-&gt;amOnPage('/triggering-ajax-requests');
    $I-&gt;waitForJqueryAjax();
    $I-&gt;see('From AJAX');</code></pre>
<h4>Parameters</h4>
<ul>
<li><code>int</code> <strong>$time</strong> - The max time to wait for AJAX requests to complete.</li></ul>


*This class extends \Codeception\Module\WebDriver*

*This class implements \Codeception\Lib\Interfaces\RequiresPackage, \Codeception\Lib\Interfaces\ConflictsWithModule, \Codeception\Lib\Interfaces\ElementLocator, \Codeception\Lib\Interfaces\PageSourceSaver, \Codeception\Lib\Interfaces\ScreenshotSaver, \Codeception\Lib\Interfaces\SessionSnapshot, \Codeception\Lib\Interfaces\MultiSession, \Codeception\Lib\Interfaces\Remote, \Codeception\Lib\Interfaces\Web*

<!--/doc-->
