---
Author: Jan Wills
GENERATOR: 'Mozilla/4.05C-SGI [en] (X11; I; IRIX 6.5 IP32) [Netscape]'
---

** ** 

 **copy**/mo\_name/master\_mo/

  mo\_name ** ** is type character, required.

  master\_mo is type character, default is '-cmo-'

  Makes an exact copy of Mesh Object, master\_mo, including all data.
  The output Mesh Object, mo\_name, will become the Current Mesh
  Object. If mo\_name is the same as master\_mo nothing happens.

  If mo\_name exists it is over written.

 **EXAMPLES:**

  **cmo/copy/mo\_tet2/mo\_tet1**

  **cmo/copy/-cmo-/mo\_tet1**

  **cmo/copy/mo\_tet2**

  **cmo/copy/mo\_tet2/-cmo-**
