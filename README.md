<code>
# jquery-recaptcha-callback
#css
<link ref="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.1.3/toastr.min.css" />

Used Libraries

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.15.1/jquery.validate.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.15.0/additional-methods.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/toastr.js/2.1.3/toastr.min.js"></script>
<form id="yourform">
  {insert fields here}
</form>


Simple and Quick Captcha validation

<script>
toastr.options = {
  "closeButton": false,
  "debug": false,
  "newestOnTop": false,
  "progressBar": false,
  "positionClass": "toast-top-center",
  "preventDuplicates": false,
  "onclick": null,
  "showDuration": "300",
  "hideDuration": "1000",
  "timeOut": "5000",
  "extendedTimeOut": "1000",
  "showEasing": "swing",
  "hideEasing": "linear",
  "showMethod": "fadeIn",
  "hideMethod": "fadeOut"
}


jQuery("#yourform").validate({
	   rules: {
	      // your rules
	   },
	   submitHandler: function (form) {
          jQuery("#bootstrapmodel").modal("show");
              setTimeout(function() {
                  createRecaptcha();
              }, 100);

              function ReCapthaCallback() {
                jQuery("#bootstrapmodel").modal("hide");
                  var Request;
                    var serializedData = jQuery("#yourform").serialize();

                    // fire off the request to /form.php
                    request = jQuery.ajax({
                            url: "insert url here",
                            type: "post",
                            data: serializedData
                    });

                    // callback handler that will be called on success
                    request.done(function (response, textStatus, jqXHR) {
                            toastr["success"]("test message", "Captcha Confirmation")
                            jQuery("#name").val('');
                            jQuery("#email").val('');
                            jQuery("#contact").val('');

                    });

                    // callback handler that will be called on failure
                    request.fail(function (jqXHR, textStatus, errorThrown) {
                            // statement here
                    });

              }

              function createRecaptcha() {
                grecaptcha.render("captcha", {sitekey: "SITE KEY HERE", theme: "light",'callback' : ReCapthaCallback,});
              }

        }
});
</script>

// Html Bootstrap modal
<div class="modal fade" id="bootstrapmodel" data-backdrop="static" data-keyboard="false">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h4 class="modal-title">Confirm Capthca</h4>
      </div>
      <div class="modal-body">
        <div class='col-lg-4'>
          <div id="captcha"></div>
        </div>
      </div>
    </div>
  </div>
</div>

	   

</code>
