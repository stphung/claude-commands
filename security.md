# Security Audit & Hardening - Custom Command for Claude Code

# Input
Additional instructions: $ARGUMENTS

## Purpose
You are tasked with conducting a comprehensive security audit of the codebase, identifying vulnerabilities, and implementing fixes while ensuring all tests continue to pass. Your goal is to improve security posture without breaking existing functionality.

## Phase 1: Initial Security Assessment

### 1.1 Dependency Vulnerability Scan
Analyze dependencies for known vulnerabilities:
- Check package managers (npm audit, pip check, cargo audit, etc.)
- Review dependency versions against security databases
- Identify outdated packages with security patches
- Check for packages with known vulnerabilities
- Verify dependency integrity (lock files, checksums)

### 1.2 Static Security Analysis
Scan codebase for common vulnerabilities:
- **Injection Flaws**: SQL, NoSQL, Command, LDAP injection risks
- **Authentication Issues**: Weak auth, missing MFA, session problems
- **Access Control**: Authorization bypasses, privilege escalation
- **Data Exposure**: Hardcoded secrets, sensitive data in logs
- **Security Misconfigurations**: Default configs, verbose errors
- **XSS Vulnerabilities**: Unescaped user input, dangerous innerHTML
- **Insecure Deserialization**: Unsafe object construction
- **Using Components with Known Vulnerabilities**
- **Insufficient Logging & Monitoring**

### 1.3 Secrets Detection
Search for exposed credentials:
- API keys and tokens
- Database credentials
- Private keys and certificates
- AWS/Cloud service credentials
- OAuth secrets
- Encryption keys
- Webhook URLs with embedded auth

### 1.4 Configuration Review
Examine security configurations:
- CORS policies
- Content Security Policy (CSP)
- HTTP security headers
- TLS/SSL configuration
- Authentication settings
- Session management
- Rate limiting implementation

## Phase 2: Code Pattern Analysis

### 2.1 Input Validation
Check all user input points:
- Form inputs and API parameters
- File uploads
- URL parameters
- Headers and cookies
- WebSocket messages
- Third-party webhooks

### 2.2 Output Encoding
Verify proper encoding for:
- HTML context (XSS prevention)
- JavaScript context
- CSS context
- URL context
- SQL queries (parameterization)
- Shell commands
- LDAP queries

### 2.3 Authentication & Authorization
Review security controls:
- Password policies and storage
- Session management
- Token generation and validation
- Role-based access control
- API authentication
- Multi-factor authentication

### 2.4 Cryptography Usage
Assess cryptographic implementations:
- Encryption algorithms and key sizes
- Random number generation
- Password hashing (bcrypt, scrypt, Argon2)
- TLS/SSL usage
- Certificate validation
- Secure key storage

## Phase 3: Testing Strategy

### 3.1 Pre-Fix Testing Baseline
Before making any changes:
```bash
# Record current test status
npm test -- --coverage
# or appropriate test command for the project

# Save baseline results
# Document any already-failing tests
# Note current coverage percentage
```

### 3.2 Security Test Development
Create security-specific tests:
- **Input Validation Tests**: Malicious input handling
- **Authentication Tests**: Auth bypass attempts
- **Authorization Tests**: Access control verification
- **Injection Tests**: SQL/XSS/Command injection attempts
- **Session Tests**: Session fixation, timeout
- **Error Handling Tests**: Information disclosure

### 3.3 Regression Prevention
Ensure fixes don't break functionality:
- Run full test suite after each fix
- Add tests for security fixes
- Verify performance isn't degraded
- Check for breaking API changes
- Test error handling paths

## Phase 4: Vulnerability Remediation

### 4.1 Fix Priority Matrix

**CRITICAL - Fix Immediately**:
- Remote code execution
- SQL injection
- Authentication bypass
- Privilege escalation
- Exposed credentials

**HIGH - Fix Within Sprint**:
- XSS vulnerabilities
- Insecure direct object references
- Missing authentication
- Weak cryptography
- Session management flaws

**MEDIUM - Fix Soon**:
- Missing security headers
- Verbose error messages
- Weak password policies
- Missing rate limiting
- Insufficient logging

**LOW - Fix When Possible**:
- Information disclosure
- Missing HSTS
- Outdated dependencies (no known exploits)
- Code quality issues

### 4.2 Fix Implementation Process
For each vulnerability:

1. **Understand the Issue**
   - Identify root cause
   - Determine attack vectors
   - Assess potential impact

2. **Design the Fix**
   - Choose secure alternative
   - Consider performance impact
   - Plan for backward compatibility

3. **Implement Safely**
   - Write fix with tests first
   - Ensure existing tests pass
   - Add security-specific tests

4. **Verify the Fix**
   - Confirm vulnerability is resolved
   - Check for regressions
   - Run full test suite
   - Perform manual testing

### 4.3 Common Fixes Reference

**SQL Injection**:
```javascript
// Vulnerable
const query = `SELECT * FROM users WHERE id = ${userId}`;

// Secure
const query = 'SELECT * FROM users WHERE id = ?';
db.query(query, [userId]);
```

**XSS Prevention**:
```javascript
// Vulnerable
element.innerHTML = userInput;

// Secure
element.textContent = userInput;
// or use proper escaping library
element.innerHTML = escapeHtml(userInput);
```

**Path Traversal**:
```javascript
// Vulnerable
const filePath = `/uploads/${req.params.filename}`;

// Secure
const filename = path.basename(req.params.filename);
const filePath = path.join('/uploads', filename);
```

## Phase 5: Security Hardening

### 5.1 Implement Security Headers
```javascript
// Example Express.js security headers
app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      scriptSrc: ["'self'", "'unsafe-inline'"],
      styleSrc: ["'self'", "'unsafe-inline'"],
      imgSrc: ["'self'", "data:", "https:"],
    },
  },
  hsts: {
    maxAge: 31536000,
    includeSubDomains: true,
    preload: true,
  },
}));
```

### 5.2 Add Security Monitoring
- Implement security event logging
- Add intrusion detection
- Set up alerting for suspicious activities
- Track failed authentication attempts
- Monitor for unusual patterns

### 5.3 Security Configuration
- Disable unnecessary features
- Remove default accounts
- Update default configurations
- Implement least privilege
- Enable security features

## Phase 6: Testing and Validation

### 6.1 Post-Fix Testing
After implementing fixes:
```bash
# Run full test suite
npm test

# Run security-specific tests
npm run test:security

# Check coverage hasn't decreased
npm test -- --coverage

# Run linting
npm run lint

# Type checking (if applicable)
npm run typecheck
```

### 6.2 Manual Security Testing
- Test authentication flows
- Verify authorization checks
- Attempt injection attacks
- Check for information disclosure
- Test rate limiting
- Verify secure headers

### 6.3 Performance Validation
Ensure security fixes don't degrade performance:
- Benchmark critical paths
- Check response times
- Monitor memory usage
- Verify database query performance

## Output Format

For each vulnerability found:

```markdown
### Vulnerability: [Name/Type]

**Severity**: [CRITICAL/HIGH/MEDIUM/LOW]
**OWASP Category**: [e.g., A01:2021 - Broken Access Control]

**Location**: 
- File: [path/to/file.js:lineNumber]
- Function: [functionName]

**Description**:
[Clear explanation of the vulnerability and its potential impact]

**Proof of Concept**:
```[language]
// Demonstration of how the vulnerability could be exploited
```

**Fix Applied**:
```diff
- // Vulnerable code
+ // Secure code
```

**Tests Added**:
```[language]
// New test cases to prevent regression
```

**Verification**:
- [ ] Vulnerability fixed
- [ ] All existing tests pass
- [ ] New security tests pass
- [ ] No performance regression
- [ ] No breaking changes
```

## Security Checklist

Before completing the audit:

- [ ] All Critical vulnerabilities fixed
- [ ] All High vulnerabilities fixed or documented
- [ ] Dependency vulnerabilities addressed
- [ ] Secrets removed from codebase
- [ ] Security headers implemented
- [ ] Input validation comprehensive
- [ ] Output encoding proper
- [ ] Authentication/authorization robust
- [ ] Cryptography properly implemented
- [ ] Security tests added
- [ ] All tests passing
- [ ] Documentation updated
- [ ] Security monitoring in place

## Anti-Patterns to Avoid

❌ **Breaking Functionality**
- Never fix security at the cost of breaking features
- Always ensure backward compatibility
- Test thoroughly before committing

❌ **Overcomplicated Fixes**
- Keep security fixes simple and maintainable
- Don't introduce unnecessary complexity
- Follow existing code patterns

❌ **Ignoring Tests**
- Never skip tests to rush security fixes
- Always add tests for security vulnerabilities
- Ensure 100% test pass rate

❌ **Security Through Obscurity**
- Don't rely on hiding implementation details
- Implement proper security controls
- Assume attackers have source code access

## Best Practices

1. **Defense in Depth**: Layer security controls
2. **Least Privilege**: Minimize access rights
3. **Fail Securely**: Errors shouldn't expose info
4. **Zero Trust**: Verify everything
5. **Keep It Simple**: Complex = vulnerable
6. **Update Regularly**: Stay current with patches

## Success Metrics

Track security improvements:
- Number of vulnerabilities fixed
- Severity reduction over time
- Test coverage for security paths
- Time to detect and fix vulnerabilities
- Successful attack prevention
- Compliance with security standards

Begin by running dependency checks and static analysis tools. Focus on fixing critical vulnerabilities first while maintaining test integrity throughout the process.