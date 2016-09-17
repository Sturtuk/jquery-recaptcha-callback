# jquery-recaptcha-callback
#css
&lt;link ref=&quot;stylesheet&quot; href=&quot;https://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.1.3/toastr.min.css&quot; /&gt;

Used Libraries

&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.15.1/jquery.validate.min.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.15.0/additional-methods.min.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;https://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.1.3/toastr.min.js&quot;&gt;&lt;/script&gt;
&lt;form id=&quot;yourform&quot;&gt;
  {insert fields here}
&lt;/form&gt;


Simple and Quick Captcha validation

&lt;script&gt;
toastr.options = {
  &quot;closeButton&quot;: false,
  &quot;debug&quot;: false,
  &quot;newestOnTop&quot;: false,
  &quot;progressBar&quot;: false,
  &quot;positionClass&quot;: &quot;toast-top-center&quot;,
  &quot;preventDuplicates&quot;: false,
  &quot;onclick&quot;: null,
  &quot;showDuration&quot;: &quot;300&quot;,
  &quot;hideDuration&quot;: &quot;1000&quot;,
  &quot;timeOut&quot;: &quot;5000&quot;,
  &quot;extendedTimeOut&quot;: &quot;1000&quot;,
  &quot;showEasing&quot;: &quot;swing&quot;,
  &quot;hideEasing&quot;: &quot;linear&quot;,
  &quot;showMethod&quot;: &quot;fadeIn&quot;,
  &quot;hideMethod&quot;: &quot;fadeOut&quot;
}


jQuery(&quot;#yourform&quot;).validate({
	   rules: {
	      // your rules
	   },
	   submitHandler: function (form) {
          jQuery(&quot;#bootstrapmodel&quot;).modal(&quot;show&quot;);
              setTimeout(function() {
                  createRecaptcha();
              }, 100);

              function ReCapthaCallback() {
                jQuery(&quot;#bootstrapmodel&quot;).modal(&quot;hide&quot;);
                  var Request;
                    var serializedData = jQuery(&quot;#yourform&quot;).serialize();

                    // fire off the request to /form.php
                    request = jQuery.ajax({
                            url: &quot;insert url here&quot;,
                            type: &quot;post&quot;,
                            data: serializedData
                    });

                    // callback handler that will be called on success
                    request.done(function (response, textStatus, jqXHR) {
                            toastr[&quot;success&quot;](&quot;test message&quot;, &quot;Captcha Confirmation&quot;)
                            jQuery(&quot;#name&quot;).val(&#39;&#39;);
                            jQuery(&quot;#email&quot;).val(&#39;&#39;);
                            jQuery(&quot;#contact&quot;).val(&#39;&#39;);

                    });

                    // callback handler that will be called on failure
                    request.fail(function (jqXHR, textStatus, errorThrown) {
                            // statement here
                    });

              }

              function createRecaptcha() {
                grecaptcha.render(&quot;captcha&quot;, {sitekey: &quot;SITE KEY HERE&quot;, theme: &quot;light&quot;,&#39;callback&#39; : ReCapthaCallback,});
              }

        }
});
&lt;/script&gt;

// Html Bootstrap modal
&lt;div class=&quot;modal fade&quot; id=&quot;bootstrapmodel&quot; data-backdrop=&quot;static&quot; data-keyboard=&quot;false&quot;&gt;
  &lt;div class=&quot;modal-dialog&quot;&gt;
    &lt;div class=&quot;modal-content&quot;&gt;
      &lt;div class=&quot;modal-header&quot;&gt;
        &lt;h4 class=&quot;modal-title&quot;&gt;Confirm Capthca&lt;/h4&gt;
      &lt;/div&gt;
      &lt;div class=&quot;modal-body&quot;&gt;
        &lt;div class=&#39;col-lg-4&#39;&gt;
          &lt;div id=&quot;captcha&quot;&gt;&lt;/div&gt;
        &lt;/div&gt;
      &lt;/div&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/div&gt;

	   
