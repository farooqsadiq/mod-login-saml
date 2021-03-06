# mod-login-saml

Copyright (C) 2017-2018 The Open Library Foundation

This software is distributed under the terms of the Apache License,
Version 2.0. See the file "[LICENSE](LICENSE)" for more information.

## Introduction

This module provides SAML2 SSO functionality for FOLIO.

### Usage

1. On Stripes UI find Settings->Organization->SSO settings, paste the IdP metadata.xml URL.
  - This configuration is stored per tenant in mod-configuration under module=LOGIN-SAML, configName=saml, code=idp.url
2. Call GET /saml/regenerate to generate keyfile with random passwords and store them in mod-configuration too.
  - Don't forget to send X-Okapi-tenant header
  - UI button will replace this manual step
  - Response is sp-metadata.xml that needs to be uploaded to IdP's configuration.
3. Make sure there is a user stored with `externalSystemId` matches `UserID` SAML attribute.
  - These default properties can be overridden by `user.property` and `saml.attribute` configuration parameters.
  - SAML binding type can be overridden by `saml.binding` configuration property, allowed values are `POST` and `REDIRECT`
  - There will be UI for these too.
4. Go back to Stripes login page (log out obviously), 'SSO Login' button show up. Clicking on it will forwarf to IdP's login page.

Endpoints are documented in [RAML file](ramls/saml-login.raml)

### Enviroment variables

`TRUST_ALL_CERTIFICATES`: if value is `true` then HTTPS certificates not checked. This is a security issue in
production environment, use it for testing only! Default value is `false`.



## Additional information

Other [modules](https://dev.folio.org/source-code/#server-side).

See project [MODLOGSAML](https://issues.folio.org/browse/MODLOGSAML)
at the [FOLIO issue tracker](https://dev.folio.org/guidelines/issue-tracker/).

Other FOLIO Developer documentation is at [dev.folio.org](https://dev.folio.org/)
