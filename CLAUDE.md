# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Streamlit-Authenticator is a secure authentication module for Streamlit applications that provides comprehensive user authentication features including login, registration, password management, and OAuth2 integration.

## Architecture

The codebase follows an MVC (Model-View-Controller) pattern:

### Core Structure
- **Views** (`streamlit_authenticator/views/`): UI components and main Authenticate class
- **Controllers** (`streamlit_authenticator/controllers/`): Business logic for authentication and cookie handling  
- **Models** (`streamlit_authenticator/models/`): Data models for authentication, cookies, OAuth2 providers (Google/Microsoft), and cloud services
- **Utilities** (`streamlit_authenticator/utilities/`): Helper functions including password hashing

### Key Components
- `Authenticate` class: Main authentication interface (imported from `streamlit_authenticator.views`)
- Configuration via YAML files (see `config.yaml` template)
- OAuth2 support for Google and Microsoft
- Two-factor authentication capabilities
- Cookie-based session management

## Development Commands

### Testing
```bash
# Run tests
pytest tests/

# Run test app
streamlit run tests/app.py
```

### Package Management
```bash
# Install development dependencies
pip install -r requirements.txt

# Install package in development mode
pip install -e .
```

### Documentation
```bash
# Build documentation (uses Sphinx)
cd docs/
pip install -r requirements.txt
# Documentation config in docs/conf.py
```

## Configuration

### Config File Structure
The application uses YAML configuration files with these main sections:
- `credentials`: User accounts with hashed passwords, roles, and metadata
- `cookie`: Session management settings (name, key, expiry)  
- `oauth2`: Google and Microsoft OAuth2 settings
- `pre-authorized`: Email whitelist for registration
- `api_key`: For two-factor authentication and cloud features

### Authentication Flow
1. Load config file with `yaml.load(file, Loader=SafeLoader)`
2. Create `stauth.Authenticate()` instance with config parameters
3. Use authentication widgets (`login()`, `register_user()`, etc.)
4. Save updated config with `yaml.dump()` after authentication changes

## Testing Architecture

- Main test application: `tests/app.py`
- Uses pytest framework (see `requirements.txt`)
- Test app demonstrates all authentication features with exception handling

## Key Development Notes

- Always update the config file after using authentication widgets
- Plain text passwords are auto-hashed unless `auto_hash=False`
- OAuth2 requires proper redirect URIs and provider-specific setup
- Session state keys: `authentication_status`, `name`, `username`, `roles`
- Multi-page apps require passing authenticator as session state variable