# Snyk Pricing Plans

## Pricing plans available

Snyk functionality is available with several [pricing plans](https://snyk.io/plans/):

* **Free**: For individual developers and small teams looking to secure while they build. Limited tests.
* **Team**: For dev teams looking to build security into their development process with shared visibility into Projects. Unlimited tests.
* **Enterprise**: Standardize dev-first security across the enterprise with centralized policy governance. Unlimited tests.

{% hint style="success" %}
[Sign up to use Snyk for free!](https://snyk.io/login?cta=sign-up\&loc=nav\&page=support\_docs\_page)
{% endhint %}

## Feature availability notice

If a feature is only available on some plans, this is shown in the feature's documentation. For example:

{% hint style="info" %}
**Feature availability**\
This feature is only available for Enterprise plans.
{% endhint %}

## Trial limitations

Snyk's 14-day trial offers a sample of the features available in the paid Enterprise plan. However, certain features will have limited functionality or be entirely unavailable in order to provide a seamless experience when the trial concludes.

If you are considering the purchase of the Team plan, remember that the trial offers features above and beyond those included in the Team plan.

The following Enterprise features are limited or unavailable during the trial:

* [**Single Sign-On (SSO)**](../enterprise-setup/using-single-sign-on-sso-for-authentication/)**:** Not available.
* [**Service Accounts**](../enterprise-setup/service-accounts.md)**:** Not available.
* [**Group / Multiple Orgs**](../snyk-admin/manage-groups-and-organizations/)**:** Limited to one Group and one Org
* [**Custom Project Tags**](../manage-issues/snyk-projects/project-tags.md)**:** Not available.
* [**Custom User Roles**](../snyk-admin/manage-users-and-permissions/member-roles.md): Not available.
* [**Audit Logging**](../snyk-admin/manage-users-and-permissions/audit-logs.md): Not available.
* [**Local Code Engine**](broken-reference/): Not available.
* [**Broker**](../enterprise-setup/snyk-broker/): Not available.
* [**Self-hosted Git**](../integrations/git-repository-scm-integrations/snyk-github-enterprise-integration.md): Not available.
* [**Private Registry Integrations**](../integrations/package-repository-integrations/): Not available.

{% hint style="info" %}
Need more help? [Contact Snyk Support](https://support.snyk.io/hc/en-us/requests/new).
{% endhint %}

I'm adding some big block of code right there

```tsx
// Some code
import * as React from 'react';
import { ImageURISource } from 'react-native';

import { sizes } from '../constants';
import { Image } from '../Image';
import { CSSIconComponent, IconComponent, IconProps } from '@gitbook/spine-icons';

/**
 * Hook to create an icon component from an "icon like" component that requires other props.
 */
export function useCreateIcon<OtherProps>(
    C: React.ComponentType<IconProps & OtherProps>,
    props: OtherProps & IconProps,
    dependencies?: any[]
): IconComponent {
    const icon = React.useCallback(
        (iconProps) => <C {...iconProps} {...props} />,
        dependencies || []
    );
    return icon;
}

/**
 * Create an icon component from an "icon like" component that requires other props.
 */
export function createIcon<OtherProps>(
    C: React.ComponentType<IconProps & OtherProps>,
    props: Partial<IconProps> & OtherProps
): IconComponent {
    return (iconProps) => <C {...iconProps} {...props} />;
}

/**
 * Convert an icon to a CSS icon.
 * It should also be used for non-svg icons in the app where only `size` is used.
 */
export function toCSSIcon(C: IconComponent): CSSIconComponent {
    return (props) => {
        if (!props.compatibilitySize) {
            throw new Error(
                'toCSSIcon: compatibilitySize is required to be passed to the CSS icon.'
            );
        }

        return <C size={props.compatibilitySize} />;
    };
}

/**
 * Render an image as an icon.
 */
export function ImageIcon(
    props: {
        source: ImageURISource;
        borderRadius?: number;
    } & IconProps
): React.ReactElement {
    const { source, size, style, dataSet, borderRadius = sizes.RADIUS_M } = props;

    return (
        <Image
            source={source}
            // @ts-ignore
            style={[{ width: size, height: size, borderRadius }, style]}
            // @ts-ignore dataSet is a RNW specific prop
            dataSet={dataSet}
        />
    );
}
```
