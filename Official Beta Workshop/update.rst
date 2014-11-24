***********************
CoreOS update procedure
***********************

CoreOS updates are done using Chrome's `Omaha Protocol`_ . The update server
knows which host runs which version of CoreOS. The update server knows if host's
updates failed etc... The paid version of CoreOS, `CoreUpdate`_ allows to
control the update procedure yourself.

A CoreOS instance always uses the same `GPT UUID`_, listed in the CoreOS
documentation. If you want to build coreOS yourself, go to  `Modifying CoreOS`_
.

If you want to try out the Omaha server yourself go to `Building Development
Images`_ . Don't forget to build your own signing keys if you are doing so.

.. links
.. _Building Development Images: https://coreos.com/docs/sdk-distributors/sdk/building-development-images/
.. _CoreUpdate: https://coreos.com/products/coreupdate/
.. _GPT UUID: https://coreos.com/docs/sdk-distributors/sdk/tips-and-tricks/#gpt-uuid-types
.. _Modifying CoreOS: https://coreos.com/docs/sdk-distributors/sdk/modifying-coreos/
.. _Omaha Protocol: https://code.google.com/p/omaha/wiki/ServerProtocol

