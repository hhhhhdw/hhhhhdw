exports.handler = async function(event, context) {
    // Allowed IP address of the company's network
    const allowedIP = '188.236.255.246';

    // Get the client's IP address
    const clientIP = event.headers['x-forwarded-for'] || event.requestContext.identity.sourceIp;

    // Check if the client's IP address matches the allowed IP
    if (clientIP === allowedIP) {
        // If it matches, redirect the user to the Google Forms link
        return {
            statusCode: 302,
            headers: {
                'Location': 'https://docs.google.com/forms/d/e/1FAIpQLSeXBj8-Aq_e9AcY-9a_RGRFg6Ht7OTADbo_2v9gnfgDgItUvA/viewform'
            }
        };
    } else {
        // If it doesn't match, show an access denied message
        return {
            statusCode: 403,
            body: 'Access Denied: You are not connected to the company\'s Wi-Fi.'
        };
    }
};
