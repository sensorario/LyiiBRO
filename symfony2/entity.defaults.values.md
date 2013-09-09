====================================
Default values of an entity atribute
====================================

If you need to get some default value of an attrbute of your entities, just
set this value in entity's class.

    class YourEntity {
        /**
         * @var boolean $open
         *
         * @ORM\Column(name="open", type="boolean")
         */
        private $open = true;
    }