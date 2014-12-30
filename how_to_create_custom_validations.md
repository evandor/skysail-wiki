# How to create custom validations

Suppose we have the following bean

    public class Password {
    	private String password;
    	private String pwdRepeated;
    }
    
Of course, entering two different values in a form for password and the repeated password should trigger a business validation violation.

### Creating a validation annotation

As the validation we want to create needs to know about more than one field, we need to create the annotation on the class level like this:

    @PasswordsMatch
    public class Password {
        (as before)
    }

The annotation itself will look something like this:

    @Constraint(validatedBy = PasswordsMatchValidator.class)
    @Target({ ElementType.TYPE })
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    public @interface PasswordsMatch {
        String message() default "The provided passwords do not match.";
        Class<?>[] groups() default { };
        Class<? extends Payload>[] payload() default { };
    }
    
### Creating the constraint validator

As you can see in the code snippet above, we are referencing a class *PasswordsMatchValidator*, 
which will do the actual validation:

    public class PasswordsMatchValidator implements ConstraintValidator<PasswordsMatch, Registrationon> {
    
        @Override
        public void initialize(PasswordsMatch passwordParameters) {
        }

        @Override
        public boolean isValid(Registration registration,ConstraintValidatorContext arg1) {
            if (registration.getPassword() == null && registration.getPwdRepeated() == null) {
                return true;
            }
            return registration.getPassword().equals(registration.getPwdRepeated());
        }
    }




