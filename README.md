//custom client_id script
<script>
function getClientId() {
  // Check if client_id cookie exists
  var clientId = document.cookie.match('(?:^|;)\\s*client_id=([^;]*)');

  if (!clientId) {
    // If client_id cookie doesn't exist, generate a new one
    var timestamp = Date.now().toString();  // Current timestamp
    var randomNumber = Math.floor(Math.random() * 10000000000);  // Random number
    clientId = 'GA1.1.' + timestamp + '.' + randomNumber;  // Format as GA1.1.<timestamp>.<random_number>
    
    // Set the client_id cookie with a 1-year expiration
    var expires = new Date();
    expires.setFullYear(expires.getFullYear() + 1);  // 1-year expiration
    document.cookie = 'client_id=' + encodeURIComponent(clientId) + '; expires=' + expires.toUTCString() + '; path=/';
  } else {
    // If cookie matches, retrieve the value from the match
    clientId = decodeURIComponent(clientId[1]);
  }

  // Remove 'GA1.1.' and format the client ID as .timestamp.random_number.
  var formattedClientId = clientId.replace('GA1.1.', '');  // Remove 'GA1.1.'
  
  // Return the formatted client ID with dots before and after
  return '.' + formattedClientId + '.';  // Format as .timestamp.random_number.
}
</script>
