# Iptables-manger-and-Firewall-for-Direct-Admin

A comprehensive DirectAdmin plugin for managing iptables firewall rules through a modern web interface.

## Features

- **Dashboard**: Real-time status monitoring and quick actions
- **Rules Management**: Add, edit, delete, and view iptables rules
- **Chains Management**: View and manage iptables chains across all tables
- **Backup System**: Create, restore, and manage iptables backups
- **Logging**: Comprehensive activity logging and system logs
- **Settings**: Configurable plugin settings and preferences
- **Security**: Secure authentication and input validation
- **Responsive Design**: Modern, mobile-friendly interface

## Requirements

- DirectAdmin 1.60 or higher
- Linux server with iptables installed
- PHP 7.4 or higher
- Root access for installation

## Installation

### Method 1: Manual Installation

1. **Download the plugin files**:
   ```bash
   cd /tmp
   wget https://github.com/grabacontroller /Iptables-manger-and-Firewall-for-Direct-Admin/main.zip
   unzip main.zip
   ```

2. **Run the installation script**:
   ```bash
   cd iptables-manager-main
   chmod +x install.sh
   sudo ./install.sh
   ```

3. **Restart DirectAdmin**:
   ```bash
   sudo service directadmin restart
   ```

### Method 2: DirectAdmin Plugin Manager

1. Log into DirectAdmin as admin
2. Go to **Advanced Features** > **Plugin Manager**
3. Click **Upload Plugin**
4. Select the plugin archive file
5. Click **Install**

## Configuration

The plugin configuration is stored in `/usr/local/directadmin/plugins/iptables-manager/conf/iptables.conf`

### Key Configuration Options

```ini
# Backup Settings
BACKUP_DIR=/usr/local/directadmin/plugins/iptables-manager/backups
MAX_BACKUPS=10
AUTO_BACKUP=yes

# Logging Settings
LOG_FILE=/usr/local/directadmin/plugins/iptables-manager/logs/iptables.log
ENABLE_LOGGING=yes
LOG_LEVEL=info

# Security Settings
DEFAULT_POLICY=DROP
CONFIRM_CHANGES=yes
```

## Usage

### Accessing the Plugin

1. Log into DirectAdmin as admin
2. Navigate to **Advanced Features** > **iptables Manager**
3. The plugin interface will load with the dashboard

### Dashboard

The dashboard provides:
- Real-time iptables status
- Active rules count
- System information
- Quick action buttons
- Recent activity feed

### Managing Rules

1. **View Rules**: Navigate to the Rules section to see all current iptables rules
2. **Add Rule**: Click "Add New Rule" and fill in the rule details
3. **Edit Rule**: Click the edit button next to any rule
4. **Delete Rule**: Click the delete button to remove a rule
5. **Filter Rules**: Use the filters to search and filter rules by table, chain, etc.

### Backup Management

1. **Create Backup**: Click "Create Backup" to save current iptables configuration
2. **Restore Backup**: Select a backup and click "Restore" to apply it
3. **Delete Backup**: Remove old backups to save space
4. **Auto Backup**: Enable automatic backups before making changes

### Chains Management

View all iptables chains organized by table:
- Filter table chains (INPUT, OUTPUT, FORWARD)
- NAT table chains
- Mangle table chains

### Logs

- **System Logs**: View plugin activity and system logs
- **Filter Logs**: Filter by log level or search terms
- **Clear Logs**: Remove old log entries

### Settings

Configure plugin behavior:
- Backup directory and retention
- Logging preferences
- Security settings
- Default policies

## Security Features

- **Authentication**: Requires DirectAdmin admin login
- **Input Validation**: All user inputs are validated and sanitized
- **Command Escaping**: Shell commands are properly escaped
- **Permission Checks**: Verifies user permissions before operations
- **Activity Logging**: All actions are logged with user attribution

## API Endpoints

The plugin provides RESTful API endpoints:

- `GET /api/status.php` - Get system status
- `GET /api/rules.php` - List all rules
- `POST /api/rules.php` - Add new rule
- `DELETE /api/rules.php` - Delete rule
- `GET /api/chains.php` - List all chains
- `GET /api/backups.php` - List backups
- `POST /api/backups.php` - Create/restore backup
- `DELETE /api/backups.php` - Delete backup
- `GET /api/logs.php` - Get logs
- `POST /api/logs.php` - Clear logs
- `GET /api/settings.php` - Get settings
- `POST /api/settings.php` - Save settings
- `GET /api/activity.php` - Get recent activity

## Troubleshooting

### Common Issues

1. **Plugin not appearing in DirectAdmin**:
   - Ensure DirectAdmin was restarted after installation
   - Check plugin permissions and ownership
   - Verify plugin is listed in `/usr/local/directadmin/data/admin/plugin_list.conf`

2. **iptables commands failing**:
   - Verify iptables is installed: `which iptables`
   - Check user permissions: ensure diradmin user can execute iptables
   - Verify kernel modules are loaded: `lsmod | grep iptable`

3. **Backup/restore issues**:
   - Check backup directory permissions
   - Verify iptables-save and iptables-restore are available
   - Check available disk space

4. **API errors**:
   - Check PHP error logs
   - Verify API file permissions
   - Ensure DirectAdmin configuration is accessible

### Log Files

- Plugin logs: `/usr/local/directadmin/plugins/iptables-manager/logs/iptables.log`
- DirectAdmin logs: `/var/log/directadmin/`
- System logs: `/var/log/messages` or `/var/log/syslog`

### Debug Mode

Enable debug logging by setting `LOG_LEVEL=debug` in the configuration file.

## Uninstallation

### Method 1: Using Uninstall Script

```bash
cd /usr/local/directadmin/plugins/iptables-manager
sudo ./uninstall.sh
```

### Method 2: Manual Removal

1. Remove plugin files:
   ```bash
   sudo rm -rf /usr/local/directadmin/plugins/iptables-manager
   ```

2. Remove from DirectAdmin:
   ```bash
   sudo sed -i '/iptables-manager=/d' /usr/local/directadmin/data/admin/plugin_list.conf
   ```

3. Restart DirectAdmin:
   ```bash
   sudo service directadmin restart
   ```

## Development

### File Structure

```
iptables-manager/
├── admin/
│   ├── index.html          # Main interface
│   ├── style.css           # Styles
│   ├── script.js           # JavaScript
│   └── api/                # API endpoints
│       ├── status.php
│       ├── rules.php
│       ├── chains.php
│       ├── backups.php
│       ├── logs.php
│       ├── settings.php
│       └── activity.php
├── user/                   # User-level interface (future)
├── conf/
│   └── iptables.conf       # Configuration
├── lang/
│   └── en.conf            # Language file
├── plugin.conf            # Plugin metadata
├── install.sh             # Installation script
├── uninstall.sh           # Uninstallation script
└── README.md              # This file
```

### Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

This plugin is licensed under the MIT License. See LICENSE file for details.

## Support

For support and bug reports:
- Create an issue on GitHub
- Contact the development team
- Check the troubleshooting section above

## Changelog

### Version 1.0.0
- Initial release
- Dashboard with status monitoring
- Rules management interface
- Backup and restore functionality
- Logging and activity tracking
- Settings configuration
- API endpoints for all operations

## Credits

Developed for DirectAdmin users who need advanced iptables management capabilities through a web interface.

---

**Note**: This plugin requires root access and modifies system firewall rules. Always test in a development environment first and ensure you have proper backups before making changes to production systems.
