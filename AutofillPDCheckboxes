<!-- START Property Match -->
<script>
document.addEventListener("DOMContentLoaded", () => {
  // Adjust this to match the slug/path of your inquiry form page
  const inquiryPage = "/private-dining-inquiry";

  // Loop through all products that might have an Add-to-Cart button
  document.querySelectorAll(".product-list, .product-detail").forEach(product => {
    const title = product.querySelector(".product-title, .product-list-item-title");
    const cartButton = product.querySelector(".sqs-button-element--primary");
    const addButton = product.querySelector(".sqs-add-to-cart-button-inner");

    if (title && addButton) {
      const titleText = title.textContent.trim();
      const [property, space] = titleText.split(" - ").map(str => str.trim());
      
      // Build a link with query params
      const newUrl = `${inquiryPage}?property=${encodeURIComponent(property)}&space=${encodeURIComponent(space)}`;
      
       // Replace label
     addButton.textContent = 'Add to Inquiry';
      
      // Prevent add-to-cart function
      addButton.addEventListener('click', function(e) {
        e.stopPropagation();
        const url = newUrl;
      window.location.href = url;
     
  }); 
    }
  	});
});
</script>
<!-- END Property Match -->

<!-- START Autofill Checkboxes -->

<script>
  function autoSelectPDCheckboxes() {
    // Get URL parameters
  const params = new URLSearchParams(window.location.search);
  const propertyParam = params.get('property') ? decodeURIComponent(params.get('property')).toLowerCase() : null;
  const spaceParam = params.get('space') ? decodeURIComponent(params.get('space')).toLowerCase() : null;

      // Find form block
  const form = document.querySelector('.fe-block-yui_3_17_2_1_1762804049203_2093');
  if (!form) {
    console.log('⏳ Form not found, retrying...');
    setTimeout(autoSelectPDCheckboxes, 300);
    return;
  }

 // Get all checkbox elements
  const checkboxes = form.querySelectorAll('input.wIoTXuBC0lMFtpfY');
  if (!checkboxes.length) {
    console.log('⚠️ No checkboxes found yet, retrying...');
    setTimeout(autoSelectPDCheckboxes, 300);
    return;
  }

  // First, simulate selecting the property
  let propertyMatched = false;
  // Match and check
  checkboxes.forEach(cb => {
    const label = cb.closest('label');
    const text = label ? label.textContent.trim().toLowerCase() : '';
    const value = cb.value.trim().toLowerCase();

    if (
      (propertyParam && (text.includes(propertyParam) || value.includes(propertyParam)))
    ) {
      cb.checked = true;
      cb.dispatchEvent(new Event('change', { bubbles: true }));
      cb.click(); // trigger Squarespace logic
      propertyMatched = true;
      console.log(`🏠 Property selected: ${value}`);
    }
  });

  // If property was matched, wait for the follow-up fieldset to load
  if (propertyMatched && spaceParam) {
    const trySelectSpace = () => {
      const spaceCheckboxes = form.querySelectorAll('input.wIoTXuBC0lMFtpfY');
      let found = false;

      spaceCheckboxes.forEach(cb => {
        const label = cb.closest('label');
        const text = label ? label.textContent.trim().toLowerCase() : '';
        const value = cb.value.trim().toLowerCase();

        if (
         (spaceParam && (text.includes(spaceParam) || value.includes(spaceParam)))
        ) {
          cb.checked = true;
      	  cb.dispatchEvent(new Event('change', { bubbles: true }));
          cb.click();
          found = true;
          console.log(`🍷 Space selected: ${value}`);
        }
      });

      if (!found) {
        console.log('⏳ Waiting for space fieldset to appear...');
        setTimeout(trySelectSpace, 500);
      }
    };

    setTimeout(trySelectSpace, 800); // delay to allow follow-up to render
  }
}

window.addEventListener('load', autoSelectPDCheckboxes);
</script>

<!-- END Autofill Checkboxes -->
